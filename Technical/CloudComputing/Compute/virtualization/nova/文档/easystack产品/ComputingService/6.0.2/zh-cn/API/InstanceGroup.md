---
title: 云主机组
---

# 云主机组列表查询
## 功能介绍
列出租户的所有云主机组。
## URI
`GET /v2.1/{project—id}/os-server-groups`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project—id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| all_projects | boolean | 否 | 仅仅管理员有权限执行。例如：GET /os-server-groups?all_projects=True |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.15"。

## 请求示例
`GET /v2.1/{project_id}/os-server-groups`
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| server_groups | array | 云主机组列表对象。 |
| id | string | 云主机组的UUID。 |
| name | string | 云主机组的名字。 |
| policies | array | 云主机组的策略。包含anti-affinity , affinity, soft-anti-affinity and soft-affinity中的一种。 |
| members | array | 云主机组中的云主机成员。 |
| metadata | object | 云主机组的元数据。 |
| project_id | string | 租户的ID。 |
| user_id | string | 用户的ID。 |

## 响应示例
```yaml
{
    "server_groups": [
        {
            "id": "616fb98f-46ca-475e-917e-2563e5a8cd19",
            "name": "test",
            "policies": ["anti-affinity"],
            "members": [],
            "metadata": {}
        }
]
}
```
## 正常响应代码
202
# 创建云主机组
## 功能介绍
创建云主机组。
## URI
`POST /v2.1/{project—id}/os-server-groups`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project—id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| name | string | 是 | 云主机组的名字。 |
| policies | array | 是 | 云主机组的策略，支持的策略：soft-anti-affinity and soft-affinity |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.15"。

## 请求示例
```yaml
{
    "server_group": {
        "name": "test",
        "policies": ["anti-affinity"]
    }
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| server_groups | array | 云主机组列表对象。 |
| id | string | 云主机组的UUID。 |
| name | string | 云主机组的名字。 |
| policies | array | 云主机组的策略。包含anti-affinity , affinity, soft-anti-affinity and soft-affinity中的一种。 |
| members | array | 云主机组中的云主机成员。 |
| metadata | object | 云主机组的元数据。 |
| project_id | string | 租户的ID。 |
| user_id | string | 用户的ID。 |

## 响应示例
```yaml
{
    "server_group": {
        "id": "ef1b7a1e-502e-45e9-9c83-de2308da8315",
        "members": [],
        "metadata": {},
        "name": "testd",
        "policies": [
            "soft-affinity"
        ],
        "project_id": "3a9a3a792b024d509d3852022b9f8436",
        "user_id": "6ebdf7c4b6e64a588d390b2325f0a0d9"
    }
}
```
## 正常响应代码
200
# 删除云主机组
## 功能介绍
删除云主机组。
## URI
`DELETE /v2.1/{project—id}/os-server-groups/{server_group_id}`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project—id | 是 | 项目ID。 |
| server_group_id | 是 | 要删除的云主机组的uuid。 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.15"。

## 请求示例
`DELETE /v2.1/3a9a3a792b024d509d3852022b9f8436/os-server-groups/ef1b7a1e-502e-45e9-9c83-de2308da8315`
## 响应消息
对DELETE操作成功的响应没有任何内容。
## 正常响应代码
204