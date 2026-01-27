---
title: 创建BFV云主机
---
# 实践场景

本文将详细介绍如何使用HTTP方式调用API创建BFV(Boot From Volume)云主机。

# 前提条件
总体上应遵循[创建云主机](../Instances.html#创建云主机)中所声明的条件及约束，确保：
* 云主机所需的镜像、计算规格、网络等资源均已准备就绪。
* 已完成 [前置条件准备](../../GettingStarted/PrerequisitePreparation.html) 操作。
* （可选）已根据需要完成 [创建可用区](../../GettingStarted/CreateAZ.html) 、 [创建SSH密钥对](../../GettingStarted/CreateSSHKeyPair.html)、[创建云主机规格](../../GettingStarted/CreateInstanceFlavor.html) 和 [创建云主机组](../../GettingStarted/CreateInstanceGroup.html) 操作。

# 操作步骤
以curl作为客户端为例，请求方式如下所示:
```
curl -g -i -X POST http://nova-api.openstack.svc.cluster.local:8774/v2.1/servers -H "X-OpenStack-Nova-API-Version: 2.67" -H "Accept: application/json" -H "Content-Type: application/json" -H "User-Agent: None" -H "X-Auth-Token: $token" -d '{"server":{"name":"new-server-test","imageRef":"","adminPass":"Easystack","block_device_mapping_v2":[{"boot_index":0,"destination_type":"volume","source_type":"image","volume_size":"50","uuid":"234121c4-8f90-4b9b-a304-b84824c79593","volume_type":"hdd"}],"flavorRef":"7","availability_zone":"default-az","OS-DCF:diskConfig":"AUTO","networks":[{"subnet_id":"a832b2c7-655c-41b5-9ac9-340796712a5e","uuid":"e825f75b-6c74-4c38-8316-07d6851654f7"}],"security_groups":[{"name":"default"}]}}'
```
其中：
* `$token`即代表上一步获取到的Token ID，可参照[签名机制](../Method.html#签名机制)中的描述获取用户Token。
* imageRef字段留空，表示不直接使用镜像创建云主机。
* block_device_mapping_v2字段指明volume的镜像源(uuid)、大小(volume_size)等信息。
* flavorRef字段即为云主机规格ID。
* networks字段指明云主机将使用的网络。

返回结果：
```json
{
	"server": {
		"id": "40d427a1-4a5b-4aec-91a0-6f018fd3ff03",
		"links": [{
			"rel": "self",
			"href": "http://nova-api.openstack.svc.cluster.local:8774/v2.1/servers/40d427a1-4a5b-4aec-91a0-6f018fd3ff03"
		}, {
			"rel": "bookmark",
			"href": "http://nova-api.openstack.svc.cluster.local:8774/servers/40d427a1-4a5b-4aec-91a0-6f018fd3ff03"
		}],
		"OS-DCF:diskConfig": "AUTO",
		"security_groups": [{
			"name": "default"
		}],
		"adminPass": "Easystack"
	}
}
```

其中：
* id字段即为创建成功的云主机id。
