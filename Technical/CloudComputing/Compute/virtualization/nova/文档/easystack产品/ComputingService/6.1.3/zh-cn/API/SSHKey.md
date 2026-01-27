---
title: SSH密钥对
---

# SSH密钥对

## 密钥对查询

### 功能介绍

查询对应账户的密钥对。
### 前提条件
云平台服务正常

### URI

`GET /v2.1/{project_id}/os-keypairs`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| user_id | string | 否 | 密钥的用户ID |
| limit  | integer | 否 | 一条请求的页面大小 |
| marker  | string | 否 | 最后可见的一条ID |



### 请求示例
`GET /v2.1/0db92f705dac4ccc97c53e518feba021/os-keypairs`

### 响应消息


| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  keypairs| object |密钥信息列表  |
|  name| string |密钥名字  |
|  public_key| string |密钥对应publicKey信息  |
|  fingerprint| integer |密钥对应指纹信息  |
|  type| integer |密钥类型，默认“ssh”  |
### 正常响应示例

```json
{
	"keypairs": [{
		"keypair": {
			"name": "lb_ssh_key-5257bfc913eb",
			"public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCnd78L2m9F9tid42HdiYXM5+jjiGM3H4x+8doqT4OF5ErLdzvjPLwG864B9wFHQZ8F5cY3s8aVrdwUwBRpTAEEtj4vvDQ1fyTQh9PZSkAmme9h5ZYyr6x98eYt1dKPUHTDiNP0mgkwojHAw/0PQWPBTCD176ZXrS9LjpJVbDZbmhXeIAEDZRyQA30ScMROKsTq4ouzpCyQdl0DPyODTP8569kzeWjphQfHKA4Tv083G5JU7+51LPZbxU3NneIlTQGyZk0A/tMTGbqVQizHUrepNugJRMvh9V8KkY6Z394IeKfRPvo1DNgnyD8GR31LldyvZGZ9zTYJPUWZVWuXDNHJ octavia@easystack.cn\n",
			"fingerprint": "86:4d:40:1f:85:b2:59:20:2a:1b:dd:1c:8e:a6:86:a1",
			"type": "ssh"
		}
	}]
}
```


### 正常响应代码

200

### 错误码

401，403

## 创建密钥对

### 功能介绍

创建密钥对。

### 前提条件

云平台服务正常。

### URI

`POST /v2.1/{project_id}/os-keypairs`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| keypair  | object | 是 | 密钥信息详情 |
| name  | string | 是 | 密钥名字 |
| public_key  | string | 否 | 密钥对应publicKey信息 |
| type  | string | 否 | 密钥类型，默认“ssh” |
| user_id | string | 否 | 密钥的用户ID |


### 请求示例
```json
{
    "keypair": {
        "name": "keypair-d20a3d59-9433-4b79-8726-20b431d89c78",
        "type": "ssh",
        "public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAgQDx8nkQv/zgGgB4rMYmIf+6A4l6Rr+o/6lHBQdW5aYd44bd8JttDCE/F/pNRr0lRE+PiqSPO8nDPHw0010JeMH9gYgnnFlyY3/OcJ02RhIPyyxYpv9FhY+2YiUkpwFOcLImyrxEsYXpD/0d3ac30bNH6Sw9JD9UZHYcpSxsIbECHw== Generated-by-Nova",
        "user_id": "fake"
    }
}
```
### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  keypairs| object |密钥信息列表  |
|  name| string |密钥名字  |
|  public_key| string |密钥对应publicKey信息  |
|  private_key| string |密钥对应privateKey信息 |
|  fingerprint| integer |密钥对应指纹信息 |
|  type| integer |密钥类型，默认“ssh” |
|  user_id| string |密钥的用户ID |

### 正常响应示例

```json
{
    "keypair": {
        "fingerprint": "1e:2c:9b:56:79:4b:45:77:f9:ca:7a:98:2c:b0:d5:3c",
        "name": "keypair-803a1926-af78-4b05-902a-1d6f7a8d9d3e",
        "type": "ssh",
        "public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAgQDx8nkQv/zgGgB4rMYmIf+6A4l6Rr+o/6lHBQdW5aYd44bd8JttDCE/F/pNRr0lRE+PiqSPO8nDPHw0010JeMH9gYgnnFlyY3/OcJ02RhIPyyxYpv9FhY+2YiUkpwFOcLImyrxEsYXpD/0d3ac30bNH6Sw9JD9UZHYcpSxsIbECHw== Generated-by-Nova",
        "user_id": "fake"
    }
}
```

### 正常响应代码

200，201

2.2版本中，状态码由200改为201。
### 错误码

401，403


## 导入密钥对

### 功能介绍

导入密钥对。
### 前提条件
● 云平台服务正常。


### URI

`POST /v2.1/{project_id}/os-keypairs`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| keypair  | object | 是 | 密钥信息详情 |
| name  | string | 是 | 密钥名字 |
| public_key  | string | 否 | 密钥对应publicKey信息 |
| type  | string | 否 | 密钥类型，默认“ssh” |
| user_id | string | 否 | 密钥的用户ID |


### 请求示例
```json
{
    "keypair": {
        "name": "keypair-d20a3d59-9433-4b79-8726-20b431d89c78",
        "type": "ssh",
        "public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAgQDx8nkQv/zgGgB4rMYmIf+6A4l6Rr+o/6lHBQdW5aYd44bd8JttDCE/F/pNRr0lRE+PiqSPO8nDPHw0010JeMH9gYgnnFlyY3/OcJ02RhIPyyxYpv9FhY+2YiUkpwFOcLImyrxEsYXpD/0d3ac30bNH6Sw9JD9UZHYcpSxsIbECHw== Generated-by-Nova",
        "user_id": "fake"
    }
}
```
### 响应消息

| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
|  keypairs| object |密钥信息列表  |
|  name| string |密钥名字  |
|  public_key| string |密钥对应publicKey信息  |
|  private_key| string |密钥对应privateKey信息 |
|  fingerprint| integer |密钥对应指纹信息 |
|  type| integer |密钥类型，默认“ssh” |
|  user_id| string |密钥的用户ID |

### 响应示例

```json
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

### 正常响应代码

200，201
2.2版本中，状态码由200改为201。

### 错误码

400，401，403，409

## 删除密钥对

### 功能介绍

删除对应账户的密钥对。
### 前提条件
● 云平台服务正常。

### URI

`DELETE /v2.1/{project_id}/os-keypairs/{keypair_name}`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
|  project_id|  是|  项目ID|
|  keypair_name|  是|  密钥对名字|

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| keypair_name   | string | 否 | 密钥对名字 |
| user_id   | string | 否 | 密钥的用户ID |

### 响应消息
没有一个成功的DELETE查询响应的内容。

### 正常响应代码

200,204

警告：
在2.2版本中，使用204作为正常返回值代码

### 错误码

401，403，404
 