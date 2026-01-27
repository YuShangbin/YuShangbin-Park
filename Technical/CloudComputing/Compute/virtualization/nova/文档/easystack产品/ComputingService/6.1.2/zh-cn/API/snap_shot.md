---
title: 云主机快照
---

# 云主机快照

## 查询云主机快照列表

### 功能介绍

列出云主机快照。

### URI

`GET /v2/images`

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| changes-since  | string | 否 | 根据镜像的最后更新时间过滤查询 |
| name  | string | 否 | 根据镜像的名称过滤查询 |
| status  | string | 否 | 根据镜像的状态进行过滤查询 |
| sort-key  | string | 否 | 设置查询的排序依据 |
| sort-dir  | string | 否 | 设置排序的方向 |
| type  | string | 否 | 根据镜像类型进行过滤查询 |
| limit  | integer | 否 | 设置查询的最大限制 |

### 请求示例
`GET /v2/images?limit=20&sort_key=name&sort_dir=asc`

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  images| array |镜像列表对象  |
|  id| string |镜像的UUID  |
|  name| string |镜像的名字  |

### 正常响应示例

```json
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


### 正常响应代码

200

### 错误码

400，401，403



## 删除云主机快照

### 功能介绍

删除云主机快照。

### URI

`DELETE /v2/images/{image_id}`

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| image_id  | string | 是 | 要删除镜像的uuid |

### 请求示例
`DELETE  /v2/images/6ff0eaa6-a444-441b-b769-78099d06f985`

### 响应消息

对DELETE操作成功的响应没有任何内容

### 正常响应代码

204

### 错误码

401，403，404
