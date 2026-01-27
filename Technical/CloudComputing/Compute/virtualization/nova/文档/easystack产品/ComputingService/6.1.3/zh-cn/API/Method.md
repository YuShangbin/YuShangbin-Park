---
title: 调用方式
---

# 请求结构
API支持基于URI发起HTTP/HTTPS GET请求。请求参数需要包含在URI中。本文列举了GET请求中的结构解释，并以云主机的服务接入地址为例进行了说明。
## 结构示例
以下为一条未编码的URI请求示例：
`http://cloud.com/v1/{project_id}/servers`
在本示例中：

- `http`指定了请求通信协议
- `cloud.com`指定了服务接入地址
- `/v1/{project_id}/servers`为资源路径，也即API访问路径
## 通信协议
支持HTTP或HTTPS协议请求通信。为了获得更高的安全性，推荐您使用HTTPS协议发送请求。涉及敏感数据时，如用户密码和SSH密钥对，推荐使用HTTPS协议。
## 服务网址
调用本文档所列举的API时均需使用OpenStack身份服务进行身份验证。 他们还需要一个从“compute”类型的标识符提取出来的“service URI”。 这将是根URI，将添加下面的每个调用来构建一个完整的路径。例如，如果“service URI”是`http://mycompute.pvt/compute/v2.1`，那么“/servers”的完整API调用是`http://mycompute.pvt/compute/v2.1/servers`。
根据部署计算服务网址可能是http或https，自定义端口，自定义路径，并包含您的租户ID。 要知道您的部署网址的唯一方法是通过使用服务目录。计算URI不应该被硬编码在应用程序中，即使他们只希望在单一地点工作。应始终从身份令牌中发现。因此，对于本文件的其余部分，我们将使用短针，其中"GET /servers"的真正含义"GET your_compute_service_URI/servers"。
## 请求方法
HTTP请求方法（也称为操作或动词），它告诉服务你正在请求什么类型的操作。

| 方法 | 说明 |
| --- | --- |
| GET | 从服务端读取指定资源的所有信息，包括数据内容和元数据（Metadata）信息，其中元数据在响应头（Response Header）中返回，数据内容在响应体（Response Body）中。 |
| PUT | 向指定的资源上传数据内容和元数据信息。如果资源已经存在，那么新上传的数据将覆盖之前的内容。 |
| POST | 向指定的资源上传数据内容。与PUT操作相比，POST的主要区别在于POST一般用来向原有的资源添加信息，而不是替换原有的内容：POST所指的资源一般是处理请求的服务，或是能够处理多块数据。 |
| DELETE | 请求服务器删除指定资源，如删除对象等。 |
| HEAD | 仅从服务端读取指定资源的元数据信息。 |

## 字符编码
请求及返回结果都使用UTF-8字符集编码。
# 公共参数
公共参数是用于标识用户和接口签名的参数，如非必要，在每个接口单独的接口文档中不再对这些参数进行说明，但每次请求均需要携带这些参数，才能正常发起请求。
## 公共请求参数
| 名称 | 类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| Host | String | 否（使用AK/SK认证时该字段必选） | 请求的服务器信息，从服务API的URI中获取。值为hostname[:port]。端口缺省时使用默认的端口，https的默认端口为443。 |
| Content-Type | String | 是 | 消息体的类型（格式）。推荐用户使用默认值application/json，有其他取值时会在具体接口中专门说明。 |
| Content-Length | String | 否 | 请求body长度，单位为Byte。 |
| X-Project-Id | String | 否 | project id，项目编号。 |
| X-Auth-Token | String | 否（使用Token认证时该字段必选） | 用户Token。用户Token也就是调用获取用户Token接口的响应值，该接口是唯一不需要认证的接口。请求响应成功后在响应消息头（Headers）中包含的“X-Subject-Token”的值即为Token值。 |
| X-OpenStack-Nova-API-Version: X.X | String | 否 | “X.X”表示调用所需的API微版本，若不指定则默认为最低版本2.1，某些调用的功能可能会受限，为保证功能完整性，我们在对应接口文档的“请求消息”部分给出了推荐设置。 |

## 公共返回参数
| 参数名称 | 参数类型 | 描述 |
| --- | --- | --- |
| RequestId | String | 请求ID。无论调用接口成功与否，都会返回该参数。 |

# 签名机制
调用接口的认证方式为Token认证，通过Token认证通用请求。
Token在计算机系统中代表令牌（临时）的意思，拥有Token就代表拥有某种权限。Token认证就是在调用API的时候将Token加到请求消息头，从而通过身份认证，获得操作API的权限。
Token可通过调用获取用户Token接口获取，调用本服务API需要project级别的Token，即调用获取用户Token接口时，请求body中`auth.scope`的取值需要选择`project`，如下所示：
```go
{
	"auth": {
		"scope": {
			"project": {
				"domain": {
					"name": "Default"
				},
				"name": "admin"
			}
		},
		"identity": {
			"password": {
				"user": {
					"password": "devstacker",
					"id": "858634b407e845f14b02bcf369225dcd0"
				}
			},
			"methods": ["password"]
		}
	}
}
```

获取Token后，再调用其他接口时，您需要在请求消息头中添加`X-Auth-Token`，其值即为`Token`。例如Token值为“ABCDEFJ....”，则调用接口时将`X-Auth-Token: ABCDEFJ....`加到请求消息头即可，如下所示:
```go
POST https://iam.cn-north-1.mycloud.com/v3/auth/projects
Content-Type: application/json
X-Auth-Token: ABCDEFJ....
```
# 返回结果
请求发送以后，您会收到响应，包含状态码、响应消息头和消息体。
状态码是一组从1xx到5xx的数字代码，状态码表示了请求响应的状态。
为了便于查看和美观，API 文档返回示例均有换行和缩进等处理，实际返回结果无换行和缩进处理。
## 正确返回结果
接口调用成功后会返回接口返回参数和请求 ID，我们称这样的返回为正常返回。HTTP 状态码为 2xx。
以云主机的接口创建云主机`（POST /v1/{project_id}/servers）`为例，若调用成功，其可能的返回如下：
```go
{
    "error": {
        "OS-DCF:diskConfig": "AUTO",
        "adminPass": "6NpUwoz2QDRN",
        "id": "f5dc173b-6804-445a-a6d8-c705dad5b5eb",
        "links": [
            {
                "href": "http://openstack.example.com/v2/6f70656e737461636b20342065766572/servers/f5dc173b-6804-445a-a6d8-c705dad5b5eb",
                "rel": "self"
            },
            {
                "href": "http://openstack.example.com/6f70656e737461636b20342065766572/servers/f5dc173b-6804-445a-a6d8-c705dad5b5eb",
                "rel": "bookmark"
            }
        ],
        "security_groups": [
            {
                "name": "default"
            }
        ]
    }
}
```

## 错误返回结果
接口调用出错后，会返回错误码、错误信息和请求 ID，我们称这样的返回为异常返回。HTTP 状态码为 4xx 或者 5xx。
```go
{
    "error": {
        "message": "The request you have made requires authentication.",
        "code": 401,
        "title": "Unauthorized"       
    }
}
```

## 公共错误码
| http状态码 | Error Message | 说明 |
| --- | --- | --- |
| 300 | multiple choices | 被请求的资源存在多个可供选择的响应。 |
| 400 | Bad Request | 服务器未能处理请求。 |
| 401 | Unauthorized | 被请求的页面需要用户名和密码。 |
| 403 | Forbidden | 对被请求页面的访问被禁止。 |
| 404 | Not Found | 服务器无法找到被请求的页面。 |
| 405 | Method Not Allowed | 请求中指定的方法不被允许。 |
| 406 | Not Acceptable | 服务器生成的响应无法被客户端所接受。 |
| 407 | Proxy Authentication Required | 用户必须首先使用代理服务器进行验证，这样请求才会被处理。 |
| 408 | Request Timeout | 请求超出了服务器的等待时间。 |
| 409 | Conflict | 由于冲突，请求无法被完成。 |
| 500 | Internal Server Error | 请求未完成。服务异常。 |
| 501 | Not Implemented | 请求未完成。服务器不支持所请求的功能。 |
| 502 | Bad Gateway | 请求未完成。服务器从上游服务器收到一个无效的响应。 |
| 503 | Service Unavailable | 请求未完成。系统暂时异常。 |
| 504 | Gateway Timeout | 网关超时。 |

