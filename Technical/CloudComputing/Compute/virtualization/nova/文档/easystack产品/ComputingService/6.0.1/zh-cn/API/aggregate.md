---
title: 可用区与主机集合
---

# 列举主机集合
## 功能介绍
列举所有主机集合。包括每个主机集合的ID，名称和可用区。
## 前提条件

- 云平台服务正常。
## URI
`GET /v2.1/{project_id}/os-aggregates`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |

## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| hosts | array | 该主机集合中的所有主机名。 |
| id | string | 主机集合ID。 |
| metadata | object | 主机集合元数据。 |
| name | string | 主机集合名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |

## 响应示例
```yaml
{
  "aggregates": [
    {
      "name": "test",
      "availability_zone": "test",
      "deleted": false,
      "created_at": "2021-02-20T08:42:06.000000",
      "updated_at": null,
      "hosts": ["fake_host1"],
      "deleted_at": null,
      "id": 1,
      "metadata": { "availability_zone": "test" }
    },
    {
      "name": "faker",
      "availability_zone": "faker_az",
      "deleted": false,
      "created_at": "2021-02-22T11:01:20.000000",
      "updated_at": null,
      "hosts": [],
      "deleted_at": null,
      "id": 4,
      "metadata": { "availability_zone": "faker_az" }
    },
    {
      "name": "tt",
      "availability_zone": "faker_az",
      "deleted": false,
      "created_at": "2021-02-22T11:05:54.000000",
      "updated_at": null,
      "hosts": ["fake_host2"],
      "deleted_at": null,
      "id": 5,
      "metadata": { "availability_zone": "faker_az" }
    }
  ]
}
```
## 正常响应代码
200
# 创建主机集合
## 功能介绍
创建一个主机集合。 如果指定了options_zone选项，则会将主机集合创建为可用区，并且可用区对普通用户可见。
## 前提条件
云平台服务正常。
## URI
POST /v2.1/{project_id}/os-aggregates

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate | object | 是 | 主机集合对象。 |
| name | string | 是 | 主机集合名字。 |
| availability_zone | string | 否 | 主机集合的可用区。 |

## 请求示例
创建一个主机集合：
```yaml
{
  "aggregate": {
    "name": "fake_name",
    "availability_zone": "nova"
  }
} 
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| id | string | 主机集合的ID。 |
| name | string | 主机集合的名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |

## 响应示例
```yaml
{
  "aggregate": {
    "name": "fake_name",
    "availability_zone": nova,
    "deleted": false,
    "created_at": "2021-02-24T06:20:43.000000",
    "updated_at": null,
    "hosts": [],
    "deleted_at": null,
    "id": 6,
    "metadata": {}
  }
}
```
## 正常响应代码
200
# 列举可用区
## 功能介绍
列举所有主机集合。包括每个主机集合的ID，名称和可用区。
## 前提条件
云平台服务正常。
## URI
`GET /v2.1/{project_id}/os-availability-zone/detail`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |

## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| availabilityZoneInfo | array | 可用区信息列表。 |
| hosts | object | 主机信息对象列表。 |
| zoneName | string | 可用区名字。 |
| zoneState | string | 可用区状态。 |
| available | boolean | True表示可用。 |

## 响应示例
```yaml
{
  "availabilityZoneInfo": [
    {
      "zoneState": { "available": true },
      "hosts": {
        "fake_host3": {
          "nova-conductor": {
            "available": true,
            "active": true,
            "updated_at": "2021-02-24T07:44:54.000000"
          },
          "nova-consoleauth": {
            "available": true,
            "active": true,
            "updated_at": "2021-02-24T07:44:52.000000"
          }
        },
        "fake_host1": {
          "nova-scheduler": {
            "available": true,
            "active": true,
            "updated_at": "2021-02-24T07:44:49.000000"
          }
        }
      },
      "zoneName": "internal"
    },
    {
      "zoneState": { "available": true },
      "hosts": {
        "fake_host2": {
          "nova-compute": {
            "available": true,
            "active": true,
            "updated_at": "2021-02-24T07:44:54.000000"
          }
        },
        "fake_host1": {
          "nova-compute": {
            "available": true,
            "active": true,
            "updated_at": "2021-02-24T07:44:54.000000"
          }
        }
      },
      "zoneName": "default-az"
    },
    {
      "zoneState": { "available": true },
      "hosts": {
        "fake_host3": {
          "nova-compute": {
            "available": true,
            "active": true,
            "updated_at": "2021-02-24T07:44:53.000000"
          }
        }
      },
      "zoneName": "faker_az"
    }
  ]
}
```
## 正常响应代码
200
# 编辑主机集合
## 功能介绍
更新集合的名称和可用性区域中的一个或两个。 如果要更新的主机聚合具有已经在给定可用性区域中的主机，则请求将失败，出现400错误。
## 前提条件

- 云平台服务正常。
## URI
`PUT /v2.1/{project_id}/os-aggregates/{aggregate_id}`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| aggregate_id | 是 | 主机集合ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate_id | string | 是 | 主机集合ID。 |
| aggregate | object | 是 | 主机集合对象。 |
| name | string | 否 | 主机集合名字。 |
| availability_zone | string | 否 | 主机集合的可用区。 |

## 请求示例
编辑一个主机集合：
```yaml
{
  "aggregate": {
    "name": "newname",
    "availability_zone": "nova2"
  }
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| hosts | array | 该主机集合中的所有主机名。 |
| id | string | 主机集合的ID。 |
| metadata | object | 主机集合的元数据。 |
| name | string | 主机集合的名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |

## 响应示例
```yaml
{
  "aggregate": {
    "name": "newname",
    "availability_zone": "nova2",
    "deleted": false,
    "created_at": "2021-02-24T06:41:41.000000",
    "updated_at": "2021-02-24T06:42:25.339149",
    "hosts": [],
    "deleted_at": null,
    "id": 8,
    "metadata": { "availability_zone": "nova2" }
  }
}
```
## 正常响应代码
200
# 删除主机集合
## 功能介绍
删除主机集合。
## 前提条件

- 云平台服务正常。
## URI
`DELETE /v2.1/{project_id}/os-aggregates/{aggregate_id}`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| aggregate_id | 是 | 主机集合ID。 |

## 响应消息
对DELETE操作成功的响应没有任何内容。
## 正常响应代码
200
# 主机集合添加主机
## 功能介绍
将主机添加到主机聚合。在请求正文中指定``add_host``操作和主机名。
## 前提条件

- 云平台服务正常。
## URI
`POST /v2.1/{project_id}/os-aggregates/{aggregate_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| aggregate_id | 是 | 主机集合ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate_id | string | 是 | 主机集合ID。 |
| add_host | object | 是 | 表示要添加主机到主机集合。 |
| host | string | 否 | 主机名。 |

## 请求示例
主机集合添加一个主机：
```yaml
{
    "add_host": {
        "host": "fake_host1"
}
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| hosts | array | 该主机集合中的所有主机名。 |
| id | string | 主机集合的ID。 |
| metadata | object | 主机集合的元数据。 |
| name | string | 主机集合的名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |

## 响应示例
```yaml
{
  "aggregate": {
    "name": "name1",
    "availability_zone": "test",
    "deleted": false,
    "created_at": "2021-02-24T06:41:41.000000",
    "updated_at": "2021-02-24T06:42:25.000000",
    "hosts": ["fake_host2"],
    "deleted_at": null,
    "id": 8,
    "metadata": { "availability_zone": "test" }
  }
}
```
## 正常响应代码
200
# 主机集合删除主机
## 功能介绍
从主机聚合中移除主机。在请求正文中指定``remove_host``操作和主机名。
## 前提条件

- 云平台服务正常。
## URI
`POST /v2.1/{project_id}/os-aggregates/{aggregate_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| aggregate_id | 是 | 主机集合ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| aggregate_id | string | 是 | 主机集合ID。 |
| remove_host | object | 是 | 表示删除主机集合中的一个主机。 |
| host | string | 否 | 主机名。 |

## 请求示例
主机集合删除一个主机：
```yaml
{
    "remove_host": {
        "host": "fake_host1"
}
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| aggregates | array | 主机集合对象。 |
| availability_zone | string | 主机集合的可用区。 |
| created_at | string | 资源创建的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted_at | string | 资源删除的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |
| deleted | boolean | 布尔值表示该资源是否删除。如果没删除，显示为false。 |
| hosts | array | 该主机集合中的所有主机名。 |
| id | string | 主机集合的ID。 |
| metadata | object | 主机集合的元数据。 |
| name | string | 主机集合的名字。 |
| updated_at | string | 资源更新的日期和时间，格式为：CCYY-MM-DDThh:mm:ss±hh:mm |

## 响应示例
```yaml
{
  "aggregate": {
    "name": "name1",
    "availability_zone": "test",
    "deleted": false,
    "created_at": "2021-02-24T06:41:41.000000",
    "updated_at": "2021-02-24T06:42:25.000000",
    "hosts": [],
    "deleted_at": null,
    "id": 8,
    "metadata": { "availability_zone": "test" }
  }
}
```
## 正常响应代码
200