---
title: 云主机回收站
---

# 查询回收站列表
## 功能介绍
列出回收站里云主机。
## URI
`GET /v2.1/{project—id}/os-server-groups`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project—id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| all_tenants  | integer | 否 | 是否查询所有项目的云主机。 |
| deleted  | boolean | 否 | 是否查询已经删除的云主机。 |

## 请求示例
`GET v2.1/3a9a3a792b024d509d3852022b9f8436/servers/detail?all_tenants=1&deleted=True`
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| servers | array | 回收站云主机列表。 |
| id | string | 云主机的UUID。 |
| name | string | 云主机的名字。 |
| status | string | 云主机的状态。 |
| locked | string | 云主机的锁定状态。 |
| deleted | string | 云主机的删除时间。 |
| metadata | object | 云主机元数据对象。 |
| user_id | string | 用户的ID。 |

## 响应示例
```yaml
{
    "images": [
        {
            "id": "70a599e0-31e7-49b7-b260-868f441e862b",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage7"
        },
        {
            "id": "155d900f-4e14-4e4c-a73d-069cbf4541e6",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage123456"
        },
        {
            "id": "a2459075-d96c-40d5-893e-577ff92e721c",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage123456"
        },
        {
            "id": "a440c04b-79fa-479c-bed1-0b816eaec379",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage6"
        },
        {
            "id": "c905cedb-7281-47e4-8a62-f26bc5fc4c77",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage123456"
        },
        {
            "id": "cedef40a-ed67-4d10-800e-17455edce175",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage123456"
        },
        {
            "id": "76fa36fc-c930-4bf3-8c8a-ea2a2420deb6",
            "links": [
                {
                    "href": "fake_href",
                    "rel": "self"
                },
                {
                    "href": "fake_href",
                    "rel": "bookmark"
                },
                {
                    "href": "fake_href",
                    "rel": "alternate",
                    "type": "application/vnd.openstack.image"
                }
            ],
            "name": "fakeimage123456"
        }
]
}
```
## 正常响应代码
200
# 恢复云主机
## 功能介绍
恢复回收站里的云主机。
## URI
`POST /v2.1/{project—id}/servers/{server_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_id | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| restore | string | 是 | 恢复云主机的动作。 |

## 请求示例
```yaml
{
    "restore": null
}
```
## 响应消息
成功提交没有返回体。
## 正常响应代码
202
# 彻底删除云主机
## 功能介绍
彻底删除回收站里的云主机。
## URI
`POST /v2.1/{project—id}/servers/{server_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_id | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| forceDelete | string | 是 | 彻底删除云主机的动作。 |

## 请求示例
```yaml
{
    "forceDelete": null
}
```
## 响应消息
成功提交没有返回体。
## 正常响应代码
202