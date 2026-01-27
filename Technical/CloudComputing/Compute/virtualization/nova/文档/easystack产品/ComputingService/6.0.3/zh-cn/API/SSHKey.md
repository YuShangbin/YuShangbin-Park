---
title: SSH密钥对
---

# 密钥对查询
## 功能介绍
查询对应账户的密钥对。
## 前提条件

- 云平台服务正常。
## URI
`GET /v2.1/{project_id}/os-keypairs`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| user_id | string | 否 | 密钥的用户ID。 |
| limit | integer | 否 | 一条请求的页面大小。 |
| marker | string | 否 | 最后可见的一条ID。 |

## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| keypairs | object | 密钥信息列表。 |
| name | string | 密钥名字。 |
| public_key | string | 密钥对应publicKey信息。 |
| fingerprint | integer | 密钥对应指纹信息。 |
| type | integer | 密钥类型，默认“ssh”。 |
| user_id | integer | 密钥的用户ID。 |

## 响应示例
```yaml
{
  "keypairs": [
    {
      "keypair": {
        "public_key": "ssh-rsa fake_key",
        "type": "ssh",
        "name": "fake_name",
        "fingerprint": "fake_fingerprint"
      }
    }
  ]
}
```
## 正常响应代码
200
# 创建密钥对
## 功能介绍
创建密钥对。
## 前提条件

- 云平台服务正常。
## URI
`POST /v2.1/{project_id}/os-keypairs`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| keypair | object | 是 | 密钥信息详情。 |
| name | string | 是 | 密钥名字。 |
| public_key | string | 否 | 密钥对应publicKey信息。 |
| type | string | 否 | 密钥类型，默认“ssh”。 |
| user_id | string | 否 | 密钥的用户ID。 |

## 请求示例
创建一个云主机规格：
```yaml
{
    "keypair": {
        "type": "ssh",
        "name": "fake_keyname"
}
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| keypairs | object | 密钥信息列表。 |
| name | string | 密钥名字。 |
| public_key | string | 密钥对应publicKey信息。 |
| private_key | string | 密钥对应privateKey信息。 |
| fingerprint | integer | 密钥对应指纹信息。 |
| type | integer | 密钥类型，默认“ssh”。 |
| user_id | integer | 密钥的用户ID。 |

## 响应示例
```yaml
{
  "keypair": {
    "public_key": "ssh-rsa fake_public_key",
    "private_key": "fake_private_key",
    "user_id": "fake_user_id",
    "name": "fake_key",
    "fingerprint": "fake_fingerprint",
    "type": "ssh"
  }
}
```
## 正常响应代码
200
# 导入密钥对
## 功能介绍
导入密钥对。
## 前提条件

- 云平台服务正常。
## URI
`POST /v2.1/{project_id}/os-keypairs`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| keypair | object | 是 | 密钥信息详情。 |
| name | string | 是 | 密钥名字。 |
| public_key | string | 否 | 密钥对应publicKey信息。 |
| type | string | 否 | 密钥类型，默认“ssh”。 |
| user_id | string | 否 | 密钥的用户ID。 |

## 请求示例
创建一个云主机规格：
```yaml
{
    "keypair": {
        "type": "ssh",
        "name": "fake_keyname",
        "public_key": "ssh-rsa fake_public_key"
}
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| keypairs | object | 密钥信息列表。 |
| name | string | 密钥名字。 |
| public_key | string | 密钥对应publicKey信息。 |
| fingerprint | integer | 密钥对应指纹信息。 |
| type | integer | 密钥类型，默认“ssh”。 |
| user_id | integer | 密钥的用户ID。 |

## 响应示例
```yaml
{
  "keypair": {
    "public_key": "ssh-rsa fake_public_key",
    "user_id": "fake_user_id",
    "name": "fake_key",
    "fingerprint": "fake_fingerprint",
    "type": "ssh"
  }
}
```
## 正常响应代码
200
# 删除密钥对
## 功能介绍
删除对应账户的密钥对。
## 前提条件

- 云平台服务正常。
## URI
`DELETE /v2.1/{project_id}/os-keypairs/{keypair_name}`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| keypair_name | 是 | 密钥对名字。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| keypair_name | string | 否 | 密钥对名字。 |
| user_id | string | 否 | 密钥的用户ID。 |

## 响应消息
没有一个成功的DELETE查询响应的内容。
## 正常响应代码
200
