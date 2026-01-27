## CFS 劣势：

​	CFS的主要缺点调度参考的因素太单一了，只有一个vruntime，这导致在稍微复杂的场景中，就需要通过 系统参数来手动干预调度，复杂度容易不受控制。还有，CFS无法考虑进程对调度延迟的需求，无论是对延迟要求高的比如交互命令，还是低要求的，都只考虑vruntime。这就导致在高负载的情况下，希望早些得到执行的任务可能会在runqueue里待很久。

```
void wake_up_new_task(struct task_struct *p)
{
	unsigned long flags;
	struct rq *rq;

	......
	activate_task(rq, p, 0); // 对于cfs，会调用到place_entity()，刚唤醒的进程会被补偿一段vruntime
	......
	check_preempt_curr(rq, p, WF_FORK);//判断这个新唤醒的进程，能否抢占当前正在运行的进程。 对于cfs会调用到check_preempt_wakeup()
	......
}
```

```
static void
place_entity(struct cfs_rq *cfs_rq, struct sched_entity *se, int initial)
{
	u64 vruntime = cfs_rq->min_vruntime;
	
	......
	if (!initial) {
		unsigned long thresh = sysctl_sched_latency;
		
		if (sched_feat(GENTLE_FAIR_SLEEPERS))
			thresh >>= 1;
		
		// 如果是睡眠后唤醒的进程，会走到这里。
		// 这里不论如何都会补偿刚被唤醒的进程一定时间，补偿的时间根据系统参数sysctl_sched_latency 调整。
		vruntime -= thresh;
	}
	
	se->vruntime = max_vruntime(se->vruntime, vruntime);
}
```

```

static void check_preempt_wakeup(struct rq *rq, struct task_struct *p, int wake_flags)
{
	struct task_struct *curr = rq->curr;
	struct sched_entity *se = &curr->se, *pse = &p->se;
	struct cfs_rq *cfs_rq = task_cfs_rq(curr);
	int scale = cfs_rq->nr_running >= sched_nr_latency;
	int next_buddy_marked = 0;

	......
	if (wakeup_preempt_entity(se, pse) == 1) {

		goto preempt;
	}
	
	return;

preempt:
	resched_curr(rq);
	......
}

static unsigned long
wakeup_gran(struct sched_entity *curr, struct sched_entity *se)
{
	unsigned long gran = sysctl_sched_wakeup_granularity;

	return calc_delta_fair(gran, se);
}

static int
wakeup_preempt_entity(struct sched_entity *curr, struct sched_entity *se)
{
	s64 gran, vdiff = curr->vruntime - se->vruntime;

	if (vdiff <= 0)
		return -1;

	gran = wakeup_gran(curr, se);
	if (vdiff > gran)
		return 1;

	return 0;
}

```

通过check_preempt_wakeup()可以看到，睡眠任务被唤醒后，判断是否可以抢占当前任务的依据是：

​	curr->vruntime - se->vruntime  >  calc_delta_fair(sysctl_sched_wakeup_granularity, se);

其中 curr是当前任务，se是刚刚唤醒的任务， se->vruntime根据上面place_entity()接口所示，等于 。cfs->min_vruntime - sysctl_sched_latency / 2.

如果满足下面这几个条件，这个依据会产生一些问题：

1. current 刚执行不久，curr->vruntime 约等于 cfs->min_vruntime
2. 两个任务的nice值都是0。

如果满足上面两个条件，那么是否可抢占的依据公式就变成下面：

​	cfs->min_vruntime - (cfs->min_vruntime - sysctl_sched_latency / 2) > sysctl_sched_wakeup_granularity

​	sysctl_sched_latency / 2 > sysctl_sched_wakeup_granularity

也就是说进程的抢占条件变得和进程本身无关了，只与系统参数的设置的大小关系有关。这会导致一些问题，如：

​	两个任务负载都不算高，经常睡眠，但是发现一个任务运行时间连1ms都不到就被抢占了，另一个任务也没有占多久，又被抢占了！两个任务就这么来回抢来抢去。

## EEVDF的解决方案：

​	eEVDF（Earliest Eligible Virtual Deadline First）在 CFS 上引入“请求大小敏感的延迟保证”。每个可运行实体计算一个“虚拟截止期”并且只有“有资格”者参与竞争，最终选择截止期最早者。 这样就有了两个参考条件，一个是vruntime，另一个是deadline time。

	1. vruntime，通过vruntime判断那些进程是Eligible的，也就是有资格参与候选。
	1. deadline time，在所有符合资格的进程中选择deadline 最早的进程。

### 什么是Eligible？	

​	大体可以总结为，在某个时间点，这个任务还没有把上次分配给它的时间用完，就为合格任务。

```
lag_i = S_i - real_time_i
```

​	S_i表示进程i在一段时间内应得的时间。 real_time_i表示进程i在这段时间内实际得到的时间。 如果lag_i >=0 就表示进程时间运行时间小于应得到的时间，就说明它可以接着运行，也就说这个进程是Eligible的。

​	有了lag_i的概念后，接下来就是确定 应得时间和实际时间的计算了。

### 进程i应得时间

​	应得时间就是 **各个进程通过权重，将真实时间s分割了**，比如两个权重为3和7的进程，经过10s后，这时虚拟时间才过去1s，理论上权重为3的应该给他3秒钟，权重为7的理论给他7s。

​	另 V = real_time/W ，real_time是真实时间，W是处于runqueue中的任务的权重和。我们把V 叫做系统虚拟时间。所以进程i的应得时间就是 Si = wi /W * real_time= V \* wi。这个公式其实就是按照任务i权重比例，获取任务i的应得时间。

### 进程i实际执行时间

​	任务i的 实际执行时间的计数方式在论文中没有提及，需要根据各自实现来确定。 在linux中 real_time_i 也就是任务i的实际执行时间，还是以cfs的vruntime的计算方式来计数：

```
/*
 * delta /= w
 */
static inline u64 calc_delta_fair(u64 delta, struct sched_entity *se)
{
	if (unlikely(se->load.weight != NICE_0_LOAD))
		delta = __calc_delta(delta, NICE_0_LOAD, &se->load);

	return delta;
}
```

​	calc_delta_fair的操作就是 delat * NICE_0_LOAD/ se->load. 简化一下，如果不考虑常量 NICE_0_LOAD， 其实就是 delta / se->load。 delta就是real_time_i，也就是说real_time_i，就是每个tick这个任务增加的实际执行时间。se->load就是wi，任务i的权重。

​	因此我们可以说vi = read_time_i / wi. 这里的vi其实就是按照cfs的vruntime对real_time换算后的时间。

### 系统虚拟时间

​	系统虚拟时间指 真实时间(注意不是某个进程的真实时间，而是整体的时间，也就是所有进程的执行时间加到一起)。 计算方式：

```
    \Sum v_i * w_i
V = -------------- 
           W
```

也就是所有running进程的真实时间加起来，然后 除以所有running进程的总权重。

不过 v_i * w_i 是可能溢出的，所以需要剪去一个偏移，公式为

```
      \Sum ((v_i - v0) + v0) * w_i   \Sum (v_i - v0) * w_i
  V = ---------------------------- = --------------------- + v0
                   W                            W
```

最终这个V的计算，体现在代码中，将其分成三部分来进行计算：

```
                     v0 := cfs_rq->min_vruntime
  \Sum (v_i - v0) * w_i := cfs_rq->avg_vruntime
               \Sum w_i := cfs_rq->avg_load
```

而将这三处统一起来的函数，为avg_vruntime

```c
u64 avg_vruntime(struct cfs_rq *cfs_rq)
{
	struct sched_entity *curr = cfs_rq->curr;
	s64 avg = cfs_rq->avg_vruntime;
	long load = cfs_rq->avg_load;

	if (curr && curr->on_rq) {
		unsigned long weight = scale_load_down(curr->load.weight);

		avg += entity_key(cfs_rq, curr) * weight;
		load += weight;
	}

	if (load) {
		/* sign flips effective floor / ceil */
		if (avg < 0)
			avg -= (load - 1);
		avg = div_s64(avg, load);
	}

	return cfs_rq->min_vruntime + avg;
}
可以看出，avg_vruntime()接口基本就是上述公式的一个计算：
      \Sum ((v_i - v0) + v0) * w_i   \Sum (v_i - v0) * w_i
  V = ---------------------------- = --------------------- + v0
                   W                            W
```

有了上面这些概念后，就可以来真正的计算lag_i了，eevdf就是通过lag_i来判断进程i是否eligible的。

### 如何判断是否为Eligible？

​	Eligible翻译为有资格的，合格的。eevdf每次选择，都会在合格的任务中选取有最早deadline的任务，所以合格，就是一个必要不充分条件，那么到底什么任务是合格任务呢？大体可以总结为，在某个时间点，这个任务还没有把上次分配给它的时间用完，就为合格任务。

判断一个任务是否合格的核心任务是entity_eligible，这个函数在选择下一个运行调度实体时被频繁使用。

```c
static inline s64 entity_key(struct cfs_rq *cfs_rq, struct sched_entity *se)
{
	return (s64)(se->vruntime - cfs_rq->min_vruntime);
}

static int vruntime_eligible(struct cfs_rq *cfs_rq, u64 vruntime)
{
	struct sched_entity *curr = cfs_rq->curr;
	s64 avg = cfs_rq->avg_vruntime;
	long load = cfs_rq->avg_load;

	if (curr && curr->on_rq) {
		unsigned long weight = scale_load_down(curr->load.weight);

		avg += entity_key(cfs_rq, curr) * weight;
		load += weight;
	}

	return avg >= (s64)(vruntime - cfs_rq->min_vruntime) * load;
}

int entity_eligible(struct cfs_rq *cfs_rq, struct sched_entity *se)
{
	return vruntime_eligible(cfs_rq, se->vruntime);
}
```

首先需要介绍lag这个概念，对于一个任务i,

```
lag_i = S_i - real_time_i
```

其中

```
S_i = w_i * V
```

w_i * V 是什么意思？在上面中，我们知道，

```
V = s/W 
通过 avg_vruntime()这个接口计算出来的就是V。
```

因此对lag_i进一步推导：

```
lag_i = S_i - s_i  = w_i*(V - v_i)  
等价于：
--> V >= v_i 时候是eligible的，也就是没有执行完限额时间，还有足够的时间配额可以用。
		\Sum (v_j - v0) * w_j
-->  ---------------------      + v0 >= v_i
					W
--> \Sum (v_j - v0)*w_j >= (v_i - v0)*(\Sum w_j)
可以看到 entity_eligible() 接口其实就是在计算这个公式
```

​	entity_eligible()只是判断了当前进程是否是eligible的，但并没有保存lag_i 的值。但是lag_i的值其实是很重要的，因为这个值反映了当前进程是 执行了过多时间还是执行了过少的时间。 当进程睡眠后被唤醒的过程中，可以根据这个信息来判断是否抢占当前进程。 通过记录这个值就可以解决上面CFS提到了两个频繁唤醒的进程无限反复抢占cpu的问题了。

内核中记录lag的部分如下

```c
static s64 entity_lag(u64 avruntime, struct sched_entity *se)
{
	s64 vlag, limit;

	vlag = avruntime - se->vruntime;
	limit = calc_delta_fair(max_t(u64, 2*se->slice, TICK_NSEC), se);

	return clamp(vlag, -limit, limit);
}

static void update_entity_lag(struct cfs_rq *cfs_rq, struct sched_entity *se)
{
	SCHED_WARN_ON(!se->on_rq);

	se->vlag = entity_lag(avg_vruntime(cfs_rq), se);
}
```

看出来，内核中记录的是vlag而不是lag，类似于vruntime，其实就是lag 除权重，

```
lag_i = S_i - s_i  = w_i*(V - v_i)
vlag_i = V - v_i
```

### 设置deadline

```c
static void update_curr(struct cfs_rq *cfs_rq)//每次tick都会执行到
{
	struct sched_entity *curr = cfs_rq->curr;
	u64 now = rq_clock_task(rq_of(cfs_rq));
	u64 delta_exec;

	if (unlikely(!curr))
		return;

	delta_exec = now - curr->exec_start;
	if (unlikely((s64)delta_exec <= 0))
		return;

	curr->exec_start = now;

	curr->sum_exec_runtime += delta_exec;
	schedstat_add(cfs_rq->exec_clock, delta_exec);

	curr->vruntime += calc_delta_fair(delta_exec, curr);
	update_deadline(cfs_rq, curr);
	update_min_vruntime(cfs_rq);

	account_cfs_rq_runtime(cfs_rq, delta_exec);
}
```

首先是计算 sum_exec_runtime 和 vruntime，这一部分和普通的cfs没有太大区别。
update_deadline 这里就不同了

```c
static void update_deadline(struct cfs_rq *cfs_rq, struct sched_entity *se)
{
    //如果还没到deadline，就继续执行
	if ((s64)(se->vruntime - se->deadline) < 0)
		return;

	se->slice = sysctl_sched_base_slice;

	/*
	 * EEVDF: vd_i = ve_i + r_i / w_i
	 */
    //这里可以看到如果进程的权重大，则deadline就会相对小，更容易被执行。
	se->deadline = se->vruntime + calc_delta_fair(se->slice, se);

	/*
	 * The task has consumed its request, reschedule.
	 */
    //当deadline 执行完了，就触发调度
	if (cfs_rq->nr_running > 1) {
		resched_curr(rq_of(cfs_rq));
		clear_buddies(cfs_rq, se);
	}
}
```

### eevdf算法中何时会触发调度

#### 核心触发流程

- 到期切换：当前任务“用完本次请求”（ vruntime >= deadline ）时重切片，并在就绪队列有多个实体时触发 resched_curr() 。
- 唤醒抢占：有新任务唤醒且它“更早虚拟截止期”并满足资格（ entity_eligible ）时，触发 resched_curr() 抢占当前任务。

到期切换的逻辑主要在 上文提到的update_curr()接口中体现，比较简单。

主要看一下唤醒抢占，唤醒抢占分为两种：

- 新任务被生成，如刚fork的任务。
- 旧任务，之前睡眠过了，又被唤醒了。

eevdf 对比cfs的一个大的改善是记录了上一次运行时的lag值，所谓lag就是 (应该执行的时间 - 实际执行的时间)。比如在10s内，runqueue的总权重是100，任务i的权重是20。则任务i的应该执行时间就是10*0.2=2s。如果任务i在上次执行的时候实际执行了3s，则lag=2-3=-1。同理如果上次执行的时候只执行了1s，则lag=2-1=1s。

上面说过，系统的虚拟时间计算方式如下：

```
      \Sum ((v_i - v0) + v0) * w_i   \Sum (v_i - v0) * w_i
  V = ---------------------------- = --------------------- + v0
                   W                            W
```

所以当vi加入或退出的时候，自然V需要变化，以任务退出为例，变化的公式是( j 指的是退出的任务)：

```
     ( \Sum (v_i - v0) * w_i)  - (v_j - v0)*w_j
 V' = ---------------------------------------------------- + v0
           ( \Sum w_i ) - w_j
```

对应内核的实现：

```
static inline s64 entity_key(struct cfs_rq *cfs_rq, struct sched_entity *se)
{
	return (s64)(se->vruntime - cfs_rq->min_vruntime);
}

static void
avg_vruntime_sub(struct cfs_rq *cfs_rq, struct sched_entity *se)
{
	unsigned long weight = scale_load_down(se->load.weight);
	s64 key = entity_key(cfs_rq, se);

	cfs_rq->avg_vruntime -= key * weight;
	cfs_rq->avg_load -= weight;
}
```

​	这个机制形象的理解如下：

- 假设 runqueue 中有 4 个任务，任务 4 长时间独占 CPU（比如跑了 10 秒）。按加权平均的定义，队列的平均虚拟时间 V 会被任务 4 的持续运行推高，通常超过任务 1/2/3 的 v_i 。因此这三个任务在“债务”意义上是合规的（ V ≥ v_i ），调度时会从它们中按“最早虚拟截止期”挑选一个执行。
- 任务4离队：如果任务 4 在跑了很久之后突然阻塞离开了 runqueue，内核会“记账”它的超前：把它的虚拟滞后 lag_i = V - v_i 记录为负值（表示它跑得超前）。同时，把它对 V 的贡献从加权平均里移除，得到新的平均 V' （只由留队任务构成）。对留下的任务而言，这等价于“先把任务 4 的影响抹去，用 V' 继续调度”。
- 对任务4的运行信息进行记账：虽然任务 4 的离队让 V 不再维持在高位（不能再直接“帮”其他任务判定为合规），但它的“超前账”已经被保存下来。等任务 4 回来时，放置逻辑会用这笔负的 lag 进行补偿，把它的 vruntime 放到更靠前的位置并设置更晚的虚拟截止期，这样它需要等到队列平均时间追平到它的“奇偶点”后才重新参与竞争，其他任务可以先行赶上。
- 简单地说，在队列里时，任务 4 的长跑会把 V 推高，让其他任务更容易被判定为合规；离队后， V 只看当前集合重算，调度像它没在一样继续，但它的“超前”不会被遗忘——会在它归队时通过滞后补偿和更晚的 deadline 体现为实际惩罚，从而把公平性补回来。假如有4个任务在runqueue中，其中任务4长时间关调度执行(比如独占cpu执行了10s)。按照上面计算V的公式：V会变成一个比较大的值，至少会比v1,v2,v3这三个任务的v值要大，因此这三个任务在未来一段时间内就一直处于eligible状态，每次调度的时候，任务1，2，3挑选一个deadline最小的放到cpu上执行即可。

​	eevdf中有一个很重要的基本性质： 永远存在一个任务i，其vi<=V。因为V是任务队列中各个任务的加权平均值，所以这是数学性质决定的。推导如下：

```
术语与定义

 偏差 δ_i ：某个值相对平均值的差，定义为 δ_i = v_i - V 。
 加权偏差和：用权重对偏差求和， Σ w_i δ_i = Σ w_i (v_i - V) 。
 加权平均 V ：按权重对 v_i 求平均， V = (Σ w_i v_i) / (Σ w_i) ，其中所有 w_i > 0 ， W = Σ w_i 。
为什么加权偏差和恒等于 0

 从定义出发：
   Σ w_i δ_i = Σ w_i (v_i - V) = Σ w_i v_i - V Σ w_i 。
   因为 V = (Σ w_i v_i) / (Σ w_i) ，所以 V Σ w_i = Σ w_i v_i 。
   于是 Σ w_i δ_i = Σ w_i v_i - Σ w_i v_i = 0 。
 这不是近似或假设，而是“加权平均”的基本性质：加权平均就是使加权偏差和为 0 的那个值。
```

​	所以从这个性质上看，虽然runqueue中任务1，2，3被任务4长时间霸占cpu，而任务4离队后其他任务还要当作什么都没发生。这样似乎有点不公平，但是其实从整体上看是合理的。因为任务4离队后，cpu并没有空闲下来，任务1，2，3依然在完全的占有cpu，不会出现所有任务都不合格导致cpu出现空转的情况。

​	而且加入任务4回来后，系统会给它惩罚，根据它的lag值决定它应该被延后执行多长时间。具体代码如下：

```
static void
place_entity(struct cfs_rq *cfs_rq, struct sched_entity *se, int flags)
{
	u64 vslice, vruntime = avg_vruntime(cfs_rq);
	s64 lag = 0;

	se->slice = sysctl_sched_base_slice;
	vslice = calc_delta_fair(se->slice, se);

	if (sched_feat(PLACE_LAG) && cfs_rq->nr_running) {
		struct sched_entity *curr = cfs_rq->curr;
		unsigned long load;

		lag = se->vlag;

		load = cfs_rq->avg_load;
		if (curr && curr->on_rq)
			load += scale_load_down(curr->load.weight);

		lag *= load + scale_load_down(se->load.weight);
		if (WARN_ON_ONCE(!load))
			load = 1;
		lag = div_s64(lag, load);
	}
	//lag值就是之前记录的账单，如果se之前执行了过长时间，这里会有一个惩罚，让它过一段时间才能上cpu执行。
	//如果se之前执行时间过少，这里会有一个奖励，让它能尽快进入cpu执行，并且执行的久一点。
	//如果是新任务，这里的lag会是0，也就是不奖励也不惩罚。
	se->vruntime = vruntime - lag;

	if (sched_feat(PLACE_DEADLINE_INITIAL) && (flags & ENQUEUE_INITIAL))
		vslice /= 2;

	/*
	 * EEVDF: vd_i = ve_i + r_i/w_i
	 */
	se->deadline = se->vruntime + vslice;
}

```

