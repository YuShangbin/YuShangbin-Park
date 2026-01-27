---
title: 可用区与主机集合
---

# 可用区与主机集合

## 列举主机集合

### 功能介绍
列举所有主机集合。包括每个主机集合的ID，名称和可用区。

### 前提条件
云平台服务正常。

### URI
示例：`GET /v2.1/{project_id}/os-aggregates`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm。 |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm。 |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| hosts | array | 该主机集合中的所有主机名。 |
| id | string | 主机集合ID。 |
| metadata | object | 主机集合元数据。 |
| name | string | 主机集合名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm。 |
| uuid | string | 主机集合的UUID。 |

### 响应示例
```json
{
    "aggregates": [
        {
            "availability_zone": "london",
            "created_at": "2016-12-27T23:47:32.911515",
            "deleted": false,
            "deleted_at": null,
            "hosts": [
                "compute"
            ],
            "id": 1,
            "metadata": {
                "availability_zone": "london"
            },
            "name": "name",
            "updated_at": null,
            "uuid": "6ba28ba7-f29b-45cc-a30b-6e3a40c2fb14"
        }
    ]
}
```

### 正常响应码
200

### 错误响应码
401，403


## 创建主机集合

### 功能介绍
创建一个主机集合。 如果指定了options_zone选项，则会将主机集合创建为可用区，并且可用区对普通用户可见。

### 前提条件
云平台服务正常。

### URI
示例：`POST /v2.1/{project_id}/os-aggregates`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate | object | 是 | 主机集合对象。 |
| name | string | 是 | 主机集合名称。 |
| availability_zone | string | 否 | 主机集合的可用区。 |

### 请求示例
```json
{
    "aggregate":
    {
        "name": "name",
        "availability_zone": "beijing"
    }
}
```

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm。 |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm。 |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| id | string | 主机集合ID。 |
| name | string | 主机集合名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm。 |
| uuid | string | 主机集合的UUID。 |

### 响应示例
```json
{
    "aggregate": {
        "availability_zone": "beijing",
        "created_at": "2016-12-27T22:51:32.877711",
        "deleted": false,
        "deleted_at": null,
        "id": 1,
        "name": "name",
        "updated_at": null,
        "uuid": "86a0da0e-9f0c-4f51-a1e0-3c25edab3783"
    }
}
```

### 正常响应码
200

### 错误响应码
400，401，403，409

## 列举可用区

### 功能介绍
列举所有主机集合。包括每个主机集合的ID，名称和可用区。

### 前提条件
云平台服务正常。

### URI
示例：`GET /v2.1/{project_id}/os-availability-zone/detail`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| availabilityZoneInfo | array | 可用区信息列表。 |
| hosts | object | 主机信息对象列表。 |
| zoneName | string | 可用区名字。 |
| zoneState | string | 可用区状态。 |
| available | boolean | True表示可用。 |

### 响应示例
```json
{
    "availabilityZoneInfo": [
        {
            "hosts": {
                "conductor": {
                    "nova-conductor": {
                        "active": true,
                        "available": true,
                        "updated_at": null
                    }
                },
                "scheduler": {
                    "nova-scheduler": {
                        "active": true,
                        "available": true,
                        "updated_at": null
                    }
                }
            },
            "zoneName": "internal",
            "zoneState": {
                "available": true
            }
        },
        {
            "hosts": {
                "compute": {
                    "nova-compute": {
                        "active": true,
                        "available": true,
                        "updated_at": null
                    }
                }
            },
            "zoneName": "nova",
            "zoneState": {
                "available": true
            }
        }
    ]
}
```

### 正常响应码
200

### 错误响应码
401，403


## 编辑主机集合

### 功能介绍
更新集合的名称和可用性区域中的一个或两个。 如果要更新的主机聚合具有已经在给定可用性区域中的主机，则请求将失败，出现400错误。

### 前提条件
云平台服务正常

### URI
示例：`PUT /v2.1/{project_id}/os-aggregates/{aggregate_id}`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|
| aggregate_id | 是 | 主机集合ID。 |

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate_id | string | 是 | 主机集合ID。 |
| aggregate | object | 是 | 主机集合对象。 |
| name | string | 是 | 主机集合名称。 |
| availability_zone | string | 否 | 主机集合的可用区。 |

### 请求示例
```json
{
    "aggregate":
    {
        "name": "newname",
        "availability_zone": "nova2"
    }
}
```

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone |	string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。|
| hosts | array | 该主机集合中的所有主机名。|
| id | string | 主机集合的ID。|
| metadata | object | 主机集合的元数据。|
| name | string | 主机集合的名字。|
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| uuid | string | 主机集合的UUID。 |

### 响应示例
```json
{
    "aggregate": {
        "availability_zone": "nova2",
        "created_at": "2016-12-27T23:47:32.897139",
        "deleted": false,
        "deleted_at": null,
        "hosts": [],
        "id": 1,
        "metadata": {
            "availability_zone": "nova2"
        },
        "name": "newname",
        "updated_at": "2016-12-27T23:47:33.067180",
        "uuid": "6f74e3f3-df28-48f3-98e1-ac941b1c5e43"
    }
}
```

### 正常响应码
200

### 错误响应码
400，401，403，404，409

## 删除主机集合

### 功能介绍
删除主机集合

### 前提条件
云平台服务正常

### URI
示例：`DELETE /v2.1/{project_id}/os-aggregates/{aggregate_id}`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|
| aggregate_id | 是 | 主机集合ID。 |

### 响应消息
对DELETE操作成功的响应没有任何内容。

### 正常响应码
200

### 错误响应码
400，401，403，404

## 主机集合添加主机

### 功能介绍
将主机添加到主机聚合。在请求正文中指定``add_host``操作和主机名。

### URI
示例：`POST /v2.1/{project_id}/os-aggregates/{aggregate_id}/action`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|
| aggregate_id | 是 | 主机集合ID。 |

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate_id | string | 是 | 主机集合ID。 |
| add_host | object | 是 | 表示要添加主机到主机集合。 |
| host | string | 否 | 主机名称。 |

### 请求示例
```json
{
    "add_host": {
        "host": "21549b2f665945baaa7101926a00143c"
    }
}
```

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone |	string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。|
| hosts | array | 该主机集合中的所有主机名。|
| id | string | 主机集合的ID。|
| metadata | object | 主机集合的元数据。|
| name | string | 主机集合的名字。|
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| uuid | string | 主机集合的UUID。 |

### 响应示例
```json
{
    "aggregate": {
        "availability_zone": "beijing",
        "created_at": "2016-12-27T23:47:30.594805",
        "deleted": false,
        "deleted_at": null,
        "hosts": [
            "compute"
        ],
        "id": 1,
        "metadata": {
            "availability_zone": "beijing"
        },
        "name": "name",
        "updated_at": null,
        "uuid": "d1842372-89c5-4fbd-ad5a-5d2e16c85456"
    }
}
```

### 正常响应码
200

### 错误响应码
400，401，403，404，409

## 主机集合删除云主机

### 功能介绍
从主机聚合中移除主机。在请求正文中指定``remove_host``操作和主机名。

### 前提条件
云平台服务正常

### URI
示例：`POST /v2.1/{project_id}/os-aggregates/{aggregate_id}/action`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|
| aggregate_id | 是 | 主机集合ID。 |

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate_id | string | 是 | 主机集合ID。 |
| remove_host | object | 是 | 表示删除主机结合中的一个主机。 |
| host | string | 否 | 主机名称。 |

### 请求示例
```json
{
    "remove_host": {
        "host": "bf1454b3d71145d49fca2101c56c728d"
    }
}
```

### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone |	string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。|
| hosts | array | 该主机集合中的所有主机名。|
| id | string | 主机集合的ID。|
| metadata | object | 主机集合的元数据。|
| name | string | 主机集合的名字。|
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| uuid | string | 主机集合的UUID。 |

### 响应示例
```json
{
    "aggregate": {
        "availability_zone": "beijing",
        "created_at": "2016-12-27T23:47:30.594805",
        "deleted": false,
        "deleted_at": null,
        "hosts": [],
        "id": 1,
        "metadata": {
            "availability_zone": "beijing"
        },
        "name": "name",
        "updated_at": null,
        "uuid": "d1842372-89c5-4fbd-ad5a-5d2e16c85456"
    }
}
```

### 正常响应码
200

### 错误响应码
400，401，403，404，409
