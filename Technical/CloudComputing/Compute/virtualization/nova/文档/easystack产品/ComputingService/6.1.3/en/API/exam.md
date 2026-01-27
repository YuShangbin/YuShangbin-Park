---
title: API文档模板
---

# 一级规格（例：云主机）

## 二级规格（例：启动云主机）

### 功能介绍

说明该操作实现的功能或效果，例：启动已停止的云主机并将其状态更改为“ACTIVE”。

### 前提条件（可选）

若执行本操作前存在必要的前提条件，请说明；若无，则删除。

### 接口约束（可选）

若执行本操作存在限制或注意事项，请说明；若无，则删除。

> 注意**接口约束**与**前提条件**的区别：

> - 前提条件强调必须先做了什么才能执行本操作；
> - 接口约束强调与本操作相关的注意，例如本操作带来的重要影响，执行本操作时不宜进行的其它操作等。

### URI

示例：`POST /v2.1/{project—id}/servers/{server_id}/action`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  |  |  |
|  |  |  |

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
|  |  |  |  |

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  |  |  |

### 请求示例

```json
POST https://{endpoint}/v1/{project_id}/cloudservers/delete
```
```json
{
    "servers": [
        {
            "id": "616fb98f-46ca-475e-917e-2563e5a8cd19"
        }
    ], 
    "delete_publicip": false, 
    "delete_volume": false
   }

```

### 正常响应示例

```json
{
	"user": {
		"name": "test_user",
		"links": {
			"self": "http://keystone-api.openstack.svc.cluster.local:35357/v3/users/5df4ae79648b4d7e954382da88cc69ef"
		},
		"extra": {
			"user_type": "individual",
			"user_role": "domain_member"
		},
		"enabled": true,
		"user_type": "individual",
		"email": null,
		"user_role": "domain_member",
		"id": "5df4ae79648b4d7e954382da88cc69ef",
		"domain_id": "default",
		"password_expires_at": null
	}
}

```


### 正常响应代码

例：200

### 错误码

例：400，401

# 修订记录

| 日期 | 修订内容 | 
| --- | --- | 
|  |  |  