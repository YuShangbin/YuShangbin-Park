---
title: 云主机规格
---

# 云主机规格

## 查询云主机规格

### 功能介绍

列出您的项目可访问的所有云主机规格

### 前提条件

云平台服务正常。

### URI

示例： `GET /v2.1/{project_id}/flavors`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| sort_key | string | 否 | 根据规格属性排序。 |
| sort_dir | string | 否 | 排序方向。 |
| limit | integer | 否 | 请求的页面大小。 |
| marker | string | 否 | 最后可见的一条ID。 |
| is_public | boolean | 否 | 只有具有管理员角色的用户才能使用，只返回具有public属性的规格。 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.61"。

### 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| flavors | array | 云主机规格列表。 |
| id | string | 云主机规格ID。 |
| name | string | 云主机规格名称。 |
| links | array | 云主机规格相关快捷链接地址。 |

### 响应示例

```json
{
  "flavors": [
    {
      "name": "1-512-20",
      "links": [
        {
          "href": "fake_href",
          "rel": "self"
        },
        {
          "href": "fake_href",
          "rel": "bookmark"
        }
      ],
      "ram": 512,
      "vcpus": 1,
      "description": null,
      "extra_specs": {},
      "swap": "",
      "os-flavor-access:is_public": true,
      "rxtx_factor": 1.0,
      "OS-FLV-EXT-DATA:ephemeral": 0,
      "disk": 0,
      "id": "1"
    },
    {
      "name": "1-1024-60",
      "links": [
        {
          "href": "fake_href",
          "rel": "self"
        },
        {
          "href": "fake_href",
          "rel": "bookmark"
        }
      ],
      "ram": 1024,
      "OS-FLV-DISABLED:disabled": false,
      "vcpus": 1,
      "description": null,
      "extra_specs": {},
      "swap": "",
      "os-flavor-access:is_public": true,
      "rxtx_factor": 1.0,
      "OS-FLV-EXT-DATA:ephemeral": 0,
      "disk": 0,
      "id": "10"
    }
  ],
  "flavors_links": [
    {
      "href": "fake_href",
      "rel": "next"
    }
  ]
}
```

### 正常响应码
200

### 错误响应码
401，403

## 创建云主机规格

### 功能介绍

创建一个云主机规格，仅适用于云管理员。

### 前提条件

云平台服务正常。

### URI

示例：`POST /v2.1/{project_id}/flavors`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id| 是 | 项目ID。|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| flavor | object | 是 | 云主机规格的ID和链接。|
| name | string | 是 | 云主机规格的名称。 |
| id | string | 否 | 云主机规格的ID，如果不提供，默认后端会生成一个uuid返回。|
| ram | integer | 是 | 云主机规格的内存大小。|
| disk | integer | 是 | 云主机规格要求的系统盘大小。 |
| vcpus | integer | 是 | 云主机规格中CPU核数。 |
| OS-FLV-EXT-DATA:ephemeral | integer | 否 | 临时盘大小。 |
| swap | integer | 否 | 交换分区大小。 |
| rxtx_factor | float | 否 | 可使用网络带宽与网络硬件带宽的比列。当前未使用该参数，默认值为1.0。 |
| os-flavor-access:is_public | boolean | 否 | 云主机规格是否为公用。 |

### 请求示例
创建一个云主机规格

```json
{
  "flavor": {
    "vcpus": 2,
    "disk": 0,
    "name": "fake_flavor",
    "os-flavor-access:is_public": true,
    "rxtx_factor": 1.0,
    "OS-FLV-EXT-DATA:ephemeral": 0,
    "ram": 1024,
    "id": null,
    "swap": 0
  }
}
```

### 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| flavor | object | 云主机规格的ID和链接。 |
| name | string | 云主机规格的名字。 |
| id | string | 云主机规格的ID。 |
| ram | integer | 云主机规格的内存大小。 |
| disk | integer | 云主机规格要求的系统盘大小。 |
| vcpus | integer | 云主机规格中CPU核数。 |
| links | array | 有关资源的链接。 |
| OS-FLV-EXT-DATA:ephemeral | integer | 临时盘大小。 |
| OS-FLV-DISABLED:disabled | boolean | 云主机规格是否禁用。 |
| swap | integer | 交换分区大小。 |
| rxtx_factor | float | 可使用网络带宽与网络硬件带宽的比例。 当前未使用该参数，默认值为1.0。 |
| os-flavor-access:is_public | boolean | 云主机规格是否为公有。 |

### 响应示例

```json
{
  "flavor": {
    "name": "fake_flavor",
    "links": [
      {
        "href": "fake_href",
        "rel": "self"
      },
      {
        "href": "fake_href",
        "rel": "bookmark"
      }
    ],
    "ram": 1024,
    "OS-FLV-DISABLED:disabled": false,
    "vcpus": 2,
    "description": null,
    "extra_specs": {},
    "swap": "",
    "os-flavor-access:is_public": true,
    "rxtx_factor": 1.0,
    "OS-FLV-EXT-DATA:ephemeral": 0,
    "disk": 0,
    "id": "fake_id"
  }
}
```

### 正常响应码
200
### 错误响应码
400，401，403，409

## 删除云主机规格

### 功能介绍
删除云主机规格。这通常是仅管理员操作。不建议删除现有云主机正在使用的flavor，因为这可能会导致在某些操作下将不正确的数据返回给用户。

### 前提条件
云平台服务正常。

### URI
示例：`DELETE /v2.1/{project_id}/flavors/{flavor_id}`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id| 是 | 项目ID。|
| flavor_id | 是 | 云主机规格ID。|

### 响应消息
成功的DELETE没有任何body内容返回。

### 正常响应码
202

### 错误响应码
400，401，403，404，409

## 编辑访问控制

### 功能介绍
编辑租户对云主机规格的访问控制权限。

### 前提条件
云平台服务正常。

### URI
示例：`POST /v2.1/{project_id}/flavors/{flavor_id}/action`

> 说明：需使用“行内代码”样式。

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id| 是 | 项目ID。|
| flavor_id | 是 | 云主机规格ID。|

### 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| flavor_id | string | 是 | 云主机规格ID。 |
| addTenantAccess | string | 是 | 添加权限操作。 |
| removeTenantAccess | string | 是 | 删除权限操作。 |
| tenant | string | 是 | 云平台租户。 |

### 请求示例
示例一：向租户添加云主机规格的访问
```json
{
    "addTenantAccess": {
        "tenant": "fake_tenant"
}
}
```
示例二：删除租户的云主机规格访问
```json
{
    "removeTenantAccess": {
        "tenant": "fake_tenant"
}
}
```

### 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| flavor_access | array | 云主机访问控制权限列表。 |
| tenant_id | string | 云平台租户ID。 |
| flavor_id | string | 云主机规格ID。 |

### 响应示例
```json
{
  "flavor_access": [
    {
      "tenant_id": "fake_tenant_id",
      "flavor_id": "fake_flavor_id"
    }
  ]
}
```

### 正常响应码

200

### 错误响应码

400，401，403，404，409
