---
title: 云主机组
---

# 云主机组

## 云主机组列表查询

### 功能介绍

列出租户的所有云主机组。

### URI

`GET /v2.1/{project—id}/os-server-groups`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| all_projects   | boolean | 否 | 仅仅管理员有权限执行。例如：GET /os-server-groups?all_projects=True |
 |limit    | integer | 否 | 设置查询的最大限制 |
 |offset    | integer | 否 | 设置查询时偏移量 |

 注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.15"。


### 请求示例
`GET /v2.1/{project_id}/os-server-groups`

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  server_groups| array |云主机组列表对象 |
|  id| string |云主机的UUID |
|  name| string |云主机组的名字  |
|  policies| array |云主机组的策略。包含anti-affinity , affinity, soft-anti-affinity and soft-affinity中的一种。  |
|  members| array |云主机组中的云主机成员  |
|  metadata| object |云主机组的元数据  |
|  project_id| string |租户的ID  |
|  user_id| string |用户的ID  |
|  rules| object |可应用于policies，目前max_server_per_host仅支持anti-affinity。max_server_per_host规则指定允许有反亲和组里有多少云主机可以在同一计算节点上。如果未指定，则只有一个云主机可以运行在反亲和性的计算节点上|


### 正常响应示例

```json
{
	"server_groups": [{
		"id": "4f72629e-35e6-40de-a648-7f4ae106a7fa",
		"name": "cloud-product-anti-group",
		"policy": "soft-anti-affinity",
		"rules": {},
		"members": ["3058bc88-126e-4142-9d36-341392990de5", "aad124e4-4ee5-4054-b76a-d643bacc5ac5", "c8df6394-58e0-46e0-9f3b-215a779b6598"],
		"project_id": "0db92f705dac4ccc97c53e518feba021",
		"user_id": "37ba0c69974e41979fc009ad372c637f"
	}]
}
```


### 正常响应代码

200

### 错误码

401，403

## 创建云主机组

### 功能介绍

创建云主机组。

### URI

`POST /v2.1/{project—id}/os-server-groups`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| name   | string | 是 | 云主机组的名字 |
| policies   | array | 是 | 云主机组的策略，支持的策略：soft-anti-affinity and soft-affinity |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.15"。

### 请求示例
```json
{
    "server_group": {
        "name": "test",
        "policies": ["soft-affinity"]
    }
}
```
### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  server_groups| array |云主机组列表对象 |
|  id| string |云主机的UUID |
|  name| string |云主机组的名字  |
|  policies| array |云主机组的策略。包含anti-affinity , affinity, soft-anti-affinity and soft-affinity中的一种。  |
|  members| array |云主机组中的云主机成员  |
|  metadata| object |云主机组的元数据  |
|  project_id| string |租户的ID  |
|  user_id| string |用户的ID  |
|  rules| object |可应用于policies，目前max_server_per_host仅支持anti-affinity。max_server_per_host规则指定允许有反亲和组里有多少云主机可以在同一计算节点上。如果未指定，则只有一个云主机可以运行在反亲和性的计算节点上|


### 正常响应示例

```json
{
	"server_groups": [{
		"id": "4f72629e-35e6-40de-a648-7f4ae106a7fa",
		"name": "cloud-product-anti-group",
		"policy": "soft-anti-affinity",
		"rules": {},
		"members": ["3058bc88-126e-4142-9d36-341392990de5", "aad124e4-4ee5-4054-b76a-d643bacc5ac5", "c8df6394-58e0-46e0-9f3b-215a779b6598"],
		"project_id": "0db92f705dac4ccc97c53e518feba021",
		"user_id": "37ba0c69974e41979fc009ad372c637f"
	}]
}
```

### 正常响应代码

200

### 错误码

400，401，403，409


## 删除云主机组

### 功能介绍

删除云主机组。

### URI

`DELETE /v2.1/{project—id}/os-server-groups/{server_group_id}`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|
|  server_group_id|  是|  要删除的云主机组的uuid|

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.15"。

### 请求示例
`DELETE /v2.1/3a9a3a792b024d509d3852022b9f8436/os-server-groups/ef1b7a1e-502e-45e9-9c83-de2308da8315`
### 响应消息

对DELETE操作成功的响应没有任何内容。

### 正常响应代码

204

### 错误码

400，401，403

