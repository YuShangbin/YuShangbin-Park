---
title: 云主机回收站
---

# 云主机回收站

## 查询回收站列表

### 功能介绍

列出回收站里云主机。

### URI

`GET /v2.1/{project_id}/servers/`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是| 项目ID |

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| all_tenants   | integer | 否 | 是否查询所有项目的云主机 |
| deleted   | boolean | 否 | 是否查询已经删除的云主机 |


### 请求示例
`GET v2.1/3a9a3a792b024d509d3852022b9f8436/servers/detail?all_tenants=1&deleted=True`

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  servers| array |回收站云主机列表 |
|  id| string |云主机的UUID |
|  name| string |云主机的名字  |
|  status| string |云主机的状态  |
|  locked| string |云主机的锁定状态  |
|  deleted| string |云主机的删除时间  |
|  metadata| object |云主机元数据对象  |
|  user_id| string |用户的ID  |
|  tenant_id| string |租户ID  |
|  hostId| string |主机id  |
|  flavor| object |云主机规格信息  |
|  image| object |镜像信息  |
|  created| string |创建时间  |
|  updated| string |更新时间  |
|  estimated_deleted| string |预计删除时间  |
|  description| string |描述  |
|  tags| string |标签  |
|  trusted_image_certificates| string |受信任镜像证书  |
|  host_status| string |主机状态  |

### 正常响应示例

```json
{
	"servers": [{
		"id": "c819da53-eedb-47ea-a305-be7dbf747c36",
		"name": "pve179",
		"status": "DELETED",
		"tenant_id": "68dd5eeecb434da0aa5ebcdda19a8db6",
		"user_id": "cb6c975e503c4b1ca741f64a42d09d50",
		"metadata": {},
		"hostId": "",
		"image": {
			"id": "4d84f09b-f41a-4dd8-9752-90adf8d709ea",
			"links": [{
				"rel": "bookmark",
				"href": "http://nova-api.openstack.svc.cluster.local:8774/0db92f705dac4ccc97c53e518feba021/images/4d84f09b-f41a-4dd8-9752-90adf8d709ea"
			}]
		},
		"flavor": {
			"id": "0f41753a-92f1-430e-8f42-3430dd514f86",
			"vcpus": 1,
			"ram": 1024,
			"disk": 20,
			"ephemeral": 0,
			"swap": 0,
			"original_name": "1c1g",
			"extra_specs": {
				"baremetal": "true"
			}
		},
		"created": "2022-04-12T06:55:45Z",
		"updated": "2022-04-12T06:56:25Z",
		"deleted": "2022-04-12T06:56:25Z",
		"estimated_deleted": "",
		"addresses": {},
		"accessIPv4": "",
		"accessIPv6": "",
		"links": [{
			"rel": "self",
			"href": "http://nova-api.openstack.svc.cluster.local:8774/v2.1/0db92f705dac4ccc97c53e518feba021/servers/c819da53-eedb-47ea-a305-be7dbf747c36"
		}, {
			"rel": "bookmark",
			"href": "http://nova-api.openstack.svc.cluster.local:8774/0db92f705dac4ccc97c53e518feba021/servers/c819da53-eedb-47ea-a305-be7dbf747c36"
		}],
		"OS-DCF:diskConfig": "AUTO",
		"OS-EXT-AZ:availability_zone": "default-az",
		"config_drive": "",
		"key_name": null,
		"OS-SRV-USG:launched_at": null,
		"OS-SRV-USG:terminated_at": "2022-04-12T06:56:25.000000",
		"OS-EXT-SRV-ATTR:host": null,
		"OS-EXT-SRV-ATTR:instance_name": "instance-0000001c",
		"OS-EXT-SRV-ATTR:hypervisor_hostname": null,
		"OS-EXT-SRV-ATTR:reservation_id": "r-5qjnjkmf",
		"OS-EXT-SRV-ATTR:launch_index": 0,
		"OS-EXT-SRV-ATTR:hostname": "pve179",
		"OS-EXT-SRV-ATTR:kernel_id": "",
		"OS-EXT-SRV-ATTR:ramdisk_id": "",
		"OS-EXT-SRV-ATTR:root_device_name": null,
		"OS-EXT-SRV-ATTR:user_data": null,
		"OS-EXT-STS:task_state": null,
		"OS-EXT-STS:vm_state": "deleted",
		"OS-EXT-STS:power_state": 0,
		"os-extended-volumes:volumes_attached": [],
		"locked": false,
		"description": null,
		"tags": [],
		"trusted_image_certificates": null,
		"host_status": ""
	}]
}

```


### 正常响应代码

200

### 错误码

400，401，403

## 恢复云主机

### 功能介绍

恢复回收站里的云主机。

### URI

`POST /v2.1/{project_id}/servers/{server_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是| 项目ID |
|  server_id|  是|  云主机的UUID。|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| restore   | string | 是 | 恢复云主机的动作 |


### 请求示例
```json
{
    "restore": null
}
```

### 响应消息

成功提交没有返回体。


### 正常响应代码

202
### 错误码

401，403，404，409

## 彻底删除云主机

### 功能介绍

彻底删除回收站里的云主机。

### URI

`POST /v2.1/{project—id}/servers/{server_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|项目ID  |
|  server_id|  是|  云主机的UUID。|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| forceDelete   | string | 是 | 彻底删除云主机的动作 |


### 请求示例
```json
{
    "forceDelete": null
}
```

### 响应消息

成功提交没有返回体。


### 正常响应代码

202
### 错误码

401，403，404，409

