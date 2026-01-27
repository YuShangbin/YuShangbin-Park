---
title: 调整云主机启动顺序
---
# 实践场景

本文将详细介绍如何使用HTTP方式调用API调整云主机启动顺序。

# 前提条件
* 云主机所在节点的计算服务状态（State）为“up”。
* 云主机状态为“active”、“pause”、“suspended”、“stopped”其中之一。
* 选择适合节点架构（x86或ARM）的ISO镜像，并成功挂载到云主机。

# 操作步骤

1. 更改云主机的Metadata顺序

调整云主机启动顺序本质上即为更改云主机`nodeinfo.com:bootorder`元数据中`order`字段的顺序，以curl作为客户端为例，先获取云主机当前的metadata，请求方式如下所示:
```
curl -g -i -X GET http://nova-api.openstack.svc.cluster.local:8774/v2.1/servers/bcc5c62a-c1e7-4204-b99a-8bb35ea4876b/metadata -H "X-OpenStack-Nova-API-Version: 2.67" -H "Accept: application/json" -H "Content-Type: application/json" -H "User-Agent: None" -H "X-Auth-Token: $token"
```
其中：
* `$token`即代表上一步获取到的Token ID，可参照[签名机制](../Method.html#签名机制)中的描述获取用户Token。

返回结果：
```json
{
	"metadata": {
		"nodeinfo.com:iso-c2f762aa-5497-4c84-ac15-211ff402fca4": "{\"image_uuid\":\"c2f762aa-5497-4c84-ac15-211ff402fca4\",\"boot_order\":1,\"image_name\":\"test-iso\"}",
		"nodeinfo.com:bootorder": "{\"order\":[\"hd\",\"cdrom\"]}"
	}
}
```

其中：
* nodeinfo.com:iso-c2f762aa-5497-4c84-ac15-211ff402fca4字段表示当前云主机已挂载ISO镜像，镜像ID为c2f762aa-5497-4c84-ac15-211ff402fca4。
* 元数据`nodeinfo.com:bootorder`的`order`字段即表示云主机的启动顺序，由此可知，hd在前，cdrom在后，云主机优先从硬盘启动。

整体更改云主机metadata，使其优先从CD-ROM启动，以curl作为客户端为例，请求方式如下所示:
```
curl -g -i -X PUT http://nova-api.openstack.svc.cluster.local:8774/v2.1/servers/bcc5c62a-c1e7-4204-b99a-8bb35ea4876b/metadata -H "X-OpenStack-Nova-API-Version: 2.67" -H "Accept: application/json" -H "Content-Type: application/json" -H "User-Agent: None" -H "X-Auth-Token: $token" -d '{"metadata":{"nodeinfo.com:iso-c2f762aa-5497-4c84-ac15-211ff402fca4":"{\"image_uuid\":\"c2f762aa-5497-4c84-ac15-211ff402fca4\",\"boot_order\":1,\"image_name\":\"test-iso\"}","nodeinfo.com:bootorder":"{\"order\":[\"cdrom\",\"hd\"]}"}}'
```

返回结果：
```json
{
	"metadata": {
		"nodeinfo.com:iso-c2f762aa-5497-4c84-ac15-211ff402fca4": "{\"image_uuid\":\"c2f762aa-5497-4c84-ac15-211ff402fca4\",\"boot_order\":1,\"image_name\":\"test-iso\"}",
		"nodeinfo.com:bootorder": "{\"order\":[\"cdrom\",\"hd\"]}"
	}
}
```

其中：
* 通过元数据`nodeinfo.com:bootorder`的`order`字段可知，cdrom在前，hd在后，云主机将优先从CD-ROM启动。

2. 硬重启云主机

调整启动顺序之后，对云主机执行硬重启操作方可生效，以curl作为客户端为例，请求方式如下所示:
```
curl -g -i -X POST http://nova-api.openstack.svc.cluster.local:8774/v2.1/servers/bcc5c62a-c1e7-4204-b99a-8bb35ea4876b/action -H "X-OpenStack-Nova-API-Version: 2.67" -H "Accept: application/json" -H "Content-Type: application/json" -H "User-Agent: None" -H "X-Auth-Token: $token" -d '{"reboot": {"type": "HARD"}}'
```
