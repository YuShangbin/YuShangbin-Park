---
title: 使用限制
---

# 针对SR-IOV网卡

* 启用SR-IOV网卡的云主机不支持外部网络、安全组、QoS、VxLAN和云主机热迁移功能。

* 在Arm架构的云平台中，飞腾不支持SR-IOV功能。鲲鹏支持SR-IOV功能，但是不支持挂起/恢复云主机，若因挂起导致云主机状态错误，请重置云主机状态，然后执行强制重启操作。

* Intel的SR-IOV网卡支持的Windows操作系统版本包括Windows Server 2019\*、Windows Server 2016\*、Windows Server 2012\*以及Windows Server 2012\* R2，为了在Windows系统的云主机中使用SR-IOV功能，您需要选择以上受支持版本的镜像，并安装相应版本的驱动程序。

* 删除启用SR-IOV网卡的云主机后，SR-IOV虚拟网卡将自动释放，但是不会被回收，可以手动删除或者绑定到其他云主机使用。

* 当云平台从V5升级至V6版本时，无论SR-IOV网卡是在升级前已插入还是升级后新插入，若需使用SR-IOV功能均请申请变更单，具体变更内容请参见运维手册中相关内容。

  当全新安装V6版本的云平台时，若在安装前已插入SR-IOV网卡，则可直接使用；若需要在安装后插入SR-IOV网卡，则请先将该操作节点置于维护模式并关机，待插入SR-IOV网卡后，再启动该节点，并申请变更单将网卡变更为UP状态。

# 针对GPU

* 在Arm架构的云平台中，不支持使用GPU功能。

* 请确保物理机BIOS中已开启Intel VT-d / AMD IOMMU功能，且物理机内核已开启IOMMU支持。

* 当使用NVIDIA vGPU时，请先参考NVIDIA官方文档提前购买许可，搭建License Server并导入许可。此外，NVIDIA vGPU功能依赖CentOS 7.6版本内核，请使用c76版本ISO。

* 目前云平台支持的GPU型号如下表所示，下述所列GPU均可用于GPU透传和虚拟化切割。支持对公网IP类型的资源计费。

<table>
<thead>
    <tr>
      <th>类型</th>
      <th>型号</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td rowspan="11">NVIDIA</td>
        <td>Tesla V100</td>
    </tr>
    <tr>
        <td>Tesla P100</td>
    </tr>
    <tr>
        <td>Tesla P40</td>
    </tr>
    <tr>
        <td>Tesla P6</td>
    </tr>
    <tr>
        <td>Tesla P4</td>
    </tr>
    <tr>
        <td>Tesla M60</td>
    </tr>
    <tr>
        <td>Tesla M10</td>
    </tr>
    <tr>
        <td>Tesla M6</td>
    </tr>
    <tr>
        <td>Tesla T4</td>
    </tr>
    <tr>
        <td>Quadro RTX 8000</td>
    </tr>
    <tr>
        <td>Quadro RTX 6000</td>
    </tr>
    <tr>
        <td>Cambricon</td>
        <td>MLU100</td>
    </tr>
</tbody></table>

# 针对在线调整云主机规格

* 在Arm架构的云平台中，不支持使用在线调整云主机规格功能。

* 云主机的操作系统必须同时支持“vCPU热添加”和“内存热添加”才能使用在线调整规格的功能。

  根据Linux和Windows的官方数据统计，具体支持情况如下（针对Linux 64位系统，只需要Kernel大于等于3.8即可，包含但不限于下表所示）：

<table>
<thead>
    <tr>
      <th>类型</th>
      <th>版本</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td rowspan="9">Linux 64位</td>
        <td>CentOS 7.x</td>
    </tr>
    <tr>
        <td>CentOS 8.x</td>
    </tr>
    <tr>
        <td>Red Hat Enterprise Linux 7.x</td>
    </tr>
    <tr>
        <td>Red Hat Enterprise Linux 8.x</td>
    </tr>
    <tr>
        <td>Ubuntu Server 14.x</td>
    </tr>
    <tr>
        <td>Ubuntu Server 16.x</td>
    </tr>
    <tr>
        <td>Ubuntu Server 17.x</td>
    </tr>
    <tr>
        <td>SUSE Linux Enterprise Server 12</td>
    </tr>
    <tr>
        <td>SUSE Linux Enterprise Server 15</td>
    </tr>
    <tr>
        <td rowspan="7">Windows Server</td>
        <td>2008 64-bit Datacenter</td>
    </tr>
    <tr>
        <td>2008 R2 Datacenter</td>
    </tr>
    <tr>
        <td>2012 Standard/Datacenter</td>
    </tr>
    <tr>
        <td>2012 R2 Standard/Datacenter</td>
    </tr>
    <tr>
        <td>2016 Standard/Datacenter</td>
    </tr>
    <tr>
        <td>2019 Standard/Datacenter</td>
    </tr>
    <tr>
        <td>2022 Standard/Datacenter</td>
    </tr>
</tbody></table>


* 目前仅支持针对通过云硬盘启动的通用计算型云主机在线调整规格。

* 只支持在线调大云主机的CPU和内存规格。

* 独享型负载均衡器不支持使用在线调整云主机规格功能。

# 针对离线调整云主机规格

* 独享型负载均衡器不支持使用离线调整云主机规格功能。

# 针对开启详细监控

通过为云主机安装并启用Agent插件，可以开启云主机详细监控展示功能，展示更丰富的监控指标（各指标的具体说明与统计方法请参考 [云主机监控](./Concepts.html#云主机监控)）。具体指标展示差异如下（其中，**√** 代表支持展示此指标，未标注代表不支持展示此指标）：

> [!WARNING]
> 由ISO格式镜像创建的云主机不支持详细监控模式，故不适用此表格。

<table>
<thead>
    <tr>
      <th colspan="2">指标</th>
      <th>详细监控模式（启用Agent）</th>
      <th>基础监控模式（未启用Agent）</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td rowspan="4">CPU</td>
        <td>CPU使用率</td>
        <td rowspan="4">√</td>
        <td>√</td>
    </tr>
    <tr>
        <td>CPU使用率- User</td>
        <td></td>
    </tr>
    <tr>
        <td>CPU使用率- System</td>
        <td></td>
    </tr>
    <tr>
        <td>CPU使用率- Interrupt</td>
        <td></td>
    </tr>
    <tr>
        <td rowspan="4">内存</td>
        <td>剩余内存</td>
        <td rowspan="4">√</td>
        <td></td>
    </tr>
    <tr>
        <td>可用内存</td>
        <td></td>
    </tr>
    <tr>
        <td>已使用内存</td>
        <td>√</td>
    </tr>
    <tr>
        <td>内存使用率</td>
        <td>√</td>
    </tr>
    <tr>
        <td rowspan="6">磁盘</td>
        <td>磁盘使用量</td>
        <td rowspan="6">√</td>
        <td></td>
    </tr>
    <tr>
        <td>磁盘使用率</td>
        <td></td>
    </tr>
    <tr>
        <td>磁盘读/写IOPS-磁盘读IOPS</td>
        <td></td>
    </tr>
    <tr>
        <td>磁盘读/写IOPS-磁盘写IOPS</td>
        <td></td>
    </tr>
    <tr>
        <td>磁盘读/写速率-磁盘读请求速率</td>
        <td>√</td>
    </tr>
    <tr>
        <td>磁盘读/写速率-磁盘写请求速率</td>
        <td>√</td>
    </tr>
    <tr>
        <td rowspan="4">网络</td>
        <td>网卡流量-网卡进流量</td>
        <td rowspan="4">√</td>
        <td>√</td>
    </tr>
    <tr>
        <td>网卡流量-网卡出流量</td>
        <td>√</td>
    </tr>
    <tr>
        <td>网卡进/出包速率-网卡进包速率</td>
        <td></td>
    </tr>
    <tr>
        <td>网卡进/出包速率-网卡出包速率</td>
        <td></td>
    </tr>
</tbody></table>
