---
title: 计算节点
---

# 计算节点

## 列举虚拟化主机及其详细信息

### 功能介绍
列出所有虚拟化主机，显示所有计算节点上所有虚拟化主机的汇总统计信息，显示虚拟化主机的详细信息。

### URI

示例：`GET /os-hypervisors/detail`

### 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| limit | integer | 否 | 限制请求返回值的数量，2.33版本新加。|
| marker | integer | 否 | 标记查询的标记位，ID作为标记。2.33版本新加，在2.52版本之前可用。 |
| marker | string | 否 | 标记查询的标记位，UUID作为标记。2.53版本新加。 |
| hypervisor_hostname_pattern | string | 否 | 根据计算节点主机名查询。2.53版本新加。|
| with_servers | boolean | 否 | 查询属于每个计算节点的所有云主机。2.53版本新加。|

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.53"。

### 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| hypervisors | array | 虚拟机监控程序的信息列表。|
| cpu_info | object | CPU的信息，包括架构、型号、供应商、特性、拓扑信息。在2.87版本之前可用。|
| current_workload | integer | 虚拟机监控程序负责的任务数。在2.87版本之前可用。|
| status | string | 虚拟机监控程序的状态，enabled或者disabled。|
| state | string | 虚拟机监控程序的状态，up或者down。 |
| dis_available_least | integer | 虚拟机监控程序的实际可用磁盘（GB）。在2.87版本之前可用。 |
| host_ip | string | 主机的IP地址。|
| free_disk_gb | integer | 剩余的可用磁盘（GB）。在2.87版本之前可用。 |
| free_ram_gb | integer | 剩余的可用内存(MB)。在2.87版本之前可用。|
| hypervisor_hostname | string | 虚拟机监控程序的名字，对于裸机来说，它是裸机节点的UUID。|
| hypervisor_type | string | 虚拟机监控程序的类型。|
| hypervisor_version | integer | 虚拟机监控程序的版本。 |
| id | integer | 虚拟机监控程序ID。在2.52版本之前可用。 |
| id | string | 虚拟机监控程序UUID。在2.53版本新加。 |
| local_gb | integer | 本地磁盘大小(GB)。在2.87版本之前可用。 |
| local_gb_used | integer | 已使用的本地盘大小(GB)。在2.87版本之前可用。 |
| memory_mb | integer | 内存(MB)大小。 在2.87版本之前可用。|
| memory_mb_used | integer | 已使用的内存(MB)大小。在2.87版本之前可用。 |
| running_vms | integer | 运行的虚拟机数量。在2.87版本之前可用。 |
| servers | array | 虚拟机监控程序上的云主机列表。在2.53版本新加。 |
| servers.uuid(Optional) | string | 云主机的ID。在2.53版本新加。 |
| servers.name(Optional) | string | 云主机的UUID。在2.53版本新加。 |
| service | object | 虚拟机监控程序服务对象。 |
| service.host | string | 虚拟机监控程序的主机名。 |
| service.id | integer | 虚拟机监控程序的服务ID。在2.52版本之前可用。 |
| service.id | string | 虚拟机监控程序的服务UUID。在2.53版本新加。 |
| service.disabled_reason | string | 禁用服务的原因。 |
| uptime | string | 虚拟机监控程序的总的运行时间和平均负载信息。在2.88版本新加。 |
| vcpus | integer | 虚拟机CPU个数。在2.87版本之前可用。 |
| cpus_used | integer | CPU已使用的数量。在2.87版本之前可用。 |
| hypervisor_links | array | 虚拟机监控程序资源的链接。在2.33版本新加。 |


### 响应示例
列举虚拟机监控程序详情(2.67版本)：
```json
{
    "hypervisors":[
        {
            "id":"a4a03c2b-9ae2-4dbc-9cc1-dbd783150268",
            "hypervisor_hostname":"node-5.domain.tld",
            "state":"up",
            "status":"disabled",
            "hypervisor_type":"QEMU",
            "hypervisor_version":4002000,
            "host_ip":"192.168.10.7",
            "service":{
                "id":"a9374fce-8976-43ae-97f1-c8d7990533ad",
                "host":"node-5.domain.tld",
                "disabled_reason":"Disabled_during_upgrading"
            },
            "vcpus":90,
            "memory_mb":522595,
            "local_gb":53119,
            "vcpus_used":51,
            "memory_mb_used":65536,
            "local_gb_used":0,
            "free_ram_mb":457059,
            "free_disk_gb":53119,
            "current_workload":0,
            "running_vms":6,
            "disk_available_least":15486,
            "cpu_allocation_ratio":2.0,
            "ram_allocation_ratio":1.0,
            "cpu_info":{
                "arch":"aarch64",
                "model":"Kunpeng-920",
                "vendor":"HiSilicon",
                "topology":{
                    "cells":4,
                    "sockets":1,
                    "cores":24,
                    "threads":1
                },
                "features":[

                ]
            }
        },
        {
            "id":"7308a9ab-b9b5-4b9f-82f3-032e88a6c71f",
            "hypervisor_hostname":"node-6.domain.tld",
            "state":"up",
            "status":"enabled",
            "hypervisor_type":"QEMU",
            "hypervisor_version":4002000,
            "host_ip":"192.168.10.8",
            "service":{
                "id":"a42744d2-4cb0-46b0-a9bd-ee84fbe3d042",
                "host":"node-6.domain.tld",
                "disabled_reason":null
            },
            "vcpus":90,
            "memory_mb":522594,
            "local_gb":53119,
            "vcpus_used":13,
            "memory_mb_used":34816,
            "local_gb_used":0,
            "free_ram_mb":487778,
            "free_disk_gb":53119,
            "current_workload":0,
            "running_vms":6,
            "disk_available_least":15486,
            "cpu_allocation_ratio":2.0,
            "ram_allocation_ratio":1.0,
            "cpu_info":{
                "arch":"aarch64",
                "model":"Kunpeng-920",
                "vendor":"HiSilicon",
                "topology":{
                    "cells":4,
                    "sockets":1,
                    "cores":24,
                    "threads":1
                },
                "features":[

                ]
            }
        }
    ]
}
```

列举虚拟机监控程序详情(2.88版本)：
```json
{
    "hypervisors": [
        {
            "host_ip": "192.168.1.135",
            "hypervisor_hostname": "host2",
            "hypervisor_type": "fake",
            "hypervisor_version": 1000,
            "id": "f6d28711-9c10-470e-8b31-c03f498b0032",
            "service": {
                "disabled_reason": null,
                "host": "host2",
                "id": "21bbb5fb-ec98-48b3-89cf-c94402c55611"
            },
            "state": "up",
            "status": "enabled",
            "uptime": null
        }
    ],
    "hypervisors_links": [
        {
            "href": "http://openstack.example.com/v2.1/6f70656e737461636b20342065766572/os-hypervisors/detail?limit=1&marker=f6d28711-9c10-470e-8b31-c03f498b0032",
            "rel": "next"
        }
    ]
}
```

### 正常响应码
200

### 错误响应码
400，401，403

## 禁用计算服务

### 功能介绍
将一个计算服务给禁用，这个计算服务将不会再被调度。

### URI
示例：`PUT /os-services/disable`

### 请求消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| host | string | 主机名 |
| binary | string | 服务名 |

### 请求示例
```json
{
    "host": "host1",
    "binary": "nova-compute"
}
```

### 响应消息
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| service | object | 服务对象 |
| binary | string | 服务名 |
| host | string | 主机名 |
| status | string | 服务状态 |

### 响应示例
```json
{
    "service": {
        "binary": "nova-compute",
        "host": "host1",
        "status": "disabled"
    }
}
```

### 正常响应码
200

### 错误响应码
400，401，403，404

## 启用计算服务

### 功能介绍
将已经禁用的计算服务启用，使其能够被调度到。

### URI
示例：`PUT /os-services/enable`

### 请求消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| host | string | 主机名 |
| binary | string | 服务名 |

### 请求示例
```json
{
    "host": "host1",
    "binary": "nova-compute"
}
```

### 响应消息
| 名称 | 类型 | 描述 |
| --- | --- | --- |
| service | object | 服务对象 |
| binary | string | 服务名 |
| host | string | 主机名 |
| status | string | 服务状态 |

### 响应示例
```json
{
    "service": {
        "binary": "nova-compute",
        "host": "host1",
        "status": "disabled"
    }
}
```

### 正常响应码
200

### 错误响应码
400，401，403，404
