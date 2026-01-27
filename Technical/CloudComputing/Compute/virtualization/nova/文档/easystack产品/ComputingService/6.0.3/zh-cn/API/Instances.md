---
title: 云主机
---

# 列举云主机
## 功能介绍
列举所有云主机和云主机相关的属性。
## 前提条件
云平台服务正常。
## URI
`GET /v2.1/{project_id}/servers`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project—id | 是 | 项目ID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| limit | integer | 否 | 查询的最大个数限制。 |
| marker | string | 否 | 最后一项的ID。 |
| sort_key | string | 否 | 按照云主机属性排序。 |
| sort_dir | string | 否 | 排序方向。 |
| changes-since | string | 否 | 根据云主机最后更改时间戳过滤查询结果。 |
| image  | string | 否 | 根据镜像的uuid过滤查询。 |
| flavor | string | 否 | 根据规格的uuid过滤查询。 |
| name | string | 否 | 可根据云主机的名字过滤查询。 |
| status | string | 否 | 根据云主机的状态过滤查询。 |
| ip | string | 否 | 根据IPv4地址过滤查询。 |
| reservation_id  | string | 否 | 服务器多次创建调用返回的保留id。 |
| all_tenants  | integer | 否 | 是否查询所有项目的云主机。 |
| deleted  | boolean | 否 | 是否查询已经删除的云主机。 |
| ip6 | string | 否 | 根据IPv6地址过滤查询。最小支持微版本2.5。 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.25"。

## 请求示例
查询云主机：
`/v2.1/{project_id}/servers/detail?all_tenants=1`

## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| servers | array | 云主机列表对象。 |
| id | string | 云主机的UUID。 |
| name | string | 云主机的名字。 |


## 响应示例
```yaml
{
  "servers": [
    {
      "OS-DCF:diskConfig": "AUTO",
      "OS-EXT-AZ:availability_zone": "default-az",
      "OS-EXT-SRV-ATTR:host": "node-2.domain.tld",
      "OS-EXT-SRV-ATTR:hostname": "faker",
      "OS-EXT-SRV-ATTR:hypervisor_hostname": "node-2.domain.tld",
      "OS-EXT-SRV-ATTR:instance_name": "instance-0000008f",
      "OS-EXT-SRV-ATTR:kernel_id": "",
      "OS-EXT-SRV-ATTR:launch_index": 0,
      "OS-EXT-SRV-ATTR:ramdisk_id": "",
      "OS-EXT-SRV-ATTR:reservation_id": "r-2ev9jgyd",
      "OS-EXT-SRV-ATTR:root_device_name": "/dev/vda",
      "OS-EXT-SRV-ATTR:user_data": "fake_user_data",
      "OS-EXT-STS:power_state": 1,
      "OS-EXT-STS:task_state": null,
      "OS-EXT-STS:vm_state": "active",
      "OS-SRV-USG:launched_at": "2021-02-23T02:09:25.000000",
      "OS-SRV-USG:terminated_at": null,
      "accessIPv4": "",
      "accessIPv6": "",
      "addresses": {
        "rally_verify_85052de9_xTCxkIeb": [
          {
            "OS-EXT-IPS-MAC:mac_addr": "fake_mac",
            "OS-EXT-IPS:type": "fixed",
            "addr": "10.2.0.7",
            "version": 4
          }
        ]
      },
      "addresses_labels_mac": ["ffake_mac"],
      "config_drive": "",
      "created": "2021-02-23T02:08:54Z",
      "deleted": "",
      "description": null,
      "estimated_deleted": "",
      "flavor": {
        "id": "212",
        "links": [
          {
            "href": "fake_href",
            "rel": "bookmark"
          }
        ]
      },
      "hostId": "fake_hostid",
      "host_status": "UP",
      "id": "ecca17b1-cb46-4efb-8ce4-2e237a3de071",
      "image": "",
      "key_name": null,
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
      "locked": false,
      "metadata": {},
      "name": "faker",
      "os-extended-volumes:volumes_attached": [
        {
          "delete_on_termination": false,
          "id": "f6790805-5ee6-43bb-8e06-c35e84fd7a17"
        },
        {
          "delete_on_termination": true,
          "id": "0ed7ad96-59a7-4987-8ec3-f993a93c8a91"
        }
      ],
      "progress": 0,
      "security_groups": [
        {
          "name": "default"
        }
      ],
      "status": "ACTIVE",
      "tags": [],
      "tenant_id": "fake_tenant_id",
      "updated": "2021-02-23T02:09:25Z",
      "user_id": "fake_user_id"
    },
    {
      "OS-DCF:diskConfig": "MANUAL",
      "OS-EXT-AZ:availability_zone": "default-az",
      "OS-EXT-SRV-ATTR:host": "node-3.domain.tld",
      "OS-EXT-SRV-ATTR:hostname": "tempest-drmulsourtest-dr-test-server-2125512491",
      "OS-EXT-SRV-ATTR:hypervisor_hostname": "node-3.domain.tld",
      "OS-EXT-SRV-ATTR:instance_name": "instance-00000083",
      "OS-EXT-SRV-ATTR:kernel_id": "",
      "OS-EXT-SRV-ATTR:launch_index": 0,
      "OS-EXT-SRV-ATTR:ramdisk_id": "",
      "OS-EXT-SRV-ATTR:reservation_id": "r-omxtvkb0",
      "OS-EXT-SRV-ATTR:root_device_name": "/dev/vda",
      "OS-EXT-SRV-ATTR:user_data": "fake_user_data",
      "OS-EXT-STS:power_state": 1,
      "OS-EXT-STS:task_state": null,
      "OS-EXT-STS:vm_state": "active",
      "OS-SRV-USG:launched_at": "2021-02-19T03:57:31.000000",
      "OS-SRV-USG:terminated_at": null,
      "accessIPv4": "",
      "accessIPv6": "",
      "addresses": {
        "tempest-DrMulSourTest-dr-test-network-1364154868": [
          {
            "OS-EXT-IPS-MAC:mac_addr": "fa:16:3e:ac:d9:a0",
            "OS-EXT-IPS:type": "fixed",
            "addr": "10.100.0.10",
            "version": 4
          }
        ]
      },
      "addresses_labels_mac": ["fa:16:3e:ac:d9:a0"],
      "config_drive": "",
      "created": "2021-02-19T03:57:03Z",
      "deleted": "",
      "description": "tempest-DrMulSourTest-dr-test-server-2125512491",
      "estimated_deleted": "",
      "flavor": {
        "id": "1",
        "links": [
          {
            "href": "fake_href",
            "rel": "bookmark"
          }
        ]
      },
      "hostId": "63d3baee6cd83965b2d64c42bd4aeb4107d22c1d615f863e28594af8",
      "host_status": "UP",
      "id": "72f63b5d-4ff4-4b6f-9fd3-97b92731d79f",
      "image": "",
      "key_name": null,
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
      "locked": false,
      "metadata": {},
      "name": "tempest-DrMulSourTest-dr-test-server-2125512491",
      "os-extended-volumes:volumes_attached": [
        {
          "delete_on_termination": true,
          "id": "09ecaef0-e752-43d3-9ff8-4dca68de3723"
        }
      ],
      "progress": 0,
      "security_groups": [
        {
          "name": "default"
        }
      ],
      "status": "ACTIVE",
      "tags": [],
      "tenant_id": "fake_tenant_id",
      "updated": "2021-02-19T11:34:02Z",
      "user_id": "fake_user_id"
    }
  ]
}
```


## 正常响应代码
200
# 创建云主机
## 功能介绍
创建一个云主机。
## 前提条件

- 用户必须有足够的云主机配额才能创建所请求的云主机数量。
- 与Image服务的连接是有效的。
## 接口约束

- 此操作的进度取决于请求镜像的位置，网络I/O，主机负载，选定的flavor和其他因素。
- 要检查请求的进度，请执行`GET / servers / {id}`请求。 此调用返回一个进度属性，该属性是从0到100的百分比值。
- Location标头将完整的URI返回给新创建的云主机，并且可以作为云主机表示中的“self”和“bookmark”链接。
- 创建云主机时，响应仅显示云主机ID，其链接和管理员密码。 您可以通过云主机上的后续`GET`请求获取其他属性。
- 在创建请求正文中包含`block-device-mapping-v2`参数，以便从卷引导云主机。
- 在创建请求正文中包含`key_name`参数，以便在创建它时向云主机添加密钥对。 要创建一个密钥对，请创建一个`create keypair http://developer.openstack.org/api-ref/compute/#create-or-import-keypair`请求。
## 故障排除

- 如果云主机状态保持“BUILDING”或显示另一个错误状态，请求失败。 确保您满足前提条件，然后调查计算节点。
- 在OpenStack Compute管理的计算节点中不创建云主机。
- 计算节点需要足够的可用资源来匹配云主机创建请求的资源。
- 确保调度程序选择过滤器可以使用与过滤器的选择条件匹配的可用计算节点来满足请求。
## 异步后置条件

- 具有正确的权限，您可以通过API调用将云主机状态看作“ACTIVE”。
- 通过正确的访问，您可以看到OpenStack Compute管理的计算节点中创建的云主机。
## URI
`POST /v2.1/{project_id}/servers`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project—id | 是 | 项目ID。该项目ID是从哪里获取的 |



## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| server | object | 是 | 要创建云主机所需的信息。 |
| flavorRef | string | 是 | 要创建云主机所使用的规格。 |
| name | string | 是 | 云主机名称。   |
| networks | array | 是 | 网络对象列表。 为租户定义了多个网络时的必需参数。 如果不指定networks参数，则云主机将连接到为当前租户创建的唯一网络。 或者，您可以在云主机上创建一个或多个NIC。 要为云主机实例提供网络的NIC，请在网络对象的uuid属性中指定网络的UUID。 要为云主机实例提供一个已存在端口的NIC，请在网络对象的port属性中指定port-id。 |
| networks.uuid | string | 否 | 要为云主机实例提供网络网卡，请在网络对象的UUID属性中指定网络的UUID。如果您省略了端口属性，则需要。从microversion 2.37开始，该值严格强制为UUID格式。 |
| networks.port | string | 否 | 要为云主机实例提供一个已存在端口的网卡，请在网络对象的port属性中指定port-id。 端口状态必须为DOWN。 如果省略uuid属性，则为必需。 所请求的安全组不应用于预先存在的端口。 |
| networks.fixed_ip | string | 否 | 网卡的IPv4地址。适用于neutron或nova-networks网络。 |
| networks.tag | string | 否 | 可应用于网络接口的设备角色标签。 |
| accessIPv4 | string | 否 | 用于访问此服务器的IPv4地址。 |
| accessIPv6 | string | 否 | 用于访问此服务器的IPv6地址。 |
| adminPass | string | 否 | 云主机的管理密码。 如果省略此参数，则该操作将生成一个新密码。 |
| availability_zone | string | 否 | 用于创建云主机的可用区域。在提供资源时，您可以指定从哪个可用分区构建实例。 |
| block_device_mapping_v2 | array | 否 | 云主机实例的卷信息。 |
| block_device_mapping_v2.boot_index | integer | 是 | 定义虚拟化层尝试从存储引导系统时尝试设备的顺序。给每个设备一个从0开始的唯一引导索引。如果要禁止设备启动，可以将启动索引设置为负值或使用默认的启动索引值None。最简单的方法是将启动设备的启动索引设置为0，其他设备使用默认的启动索引值None。一些虚拟化层可能不支持从多个设备启动;这些虚拟化层只考虑引导索引为0的设备。一些虚拟化层支持从多个设备启动，但只有在设备类型不同的情况下才支持。例如，磁盘和CD-ROM。 |
| block_device_mapping_v2.delete_on_termination | boolean | 否 | 如果要在云主机被销毁时删除对应的存储设备，请指定true。否则,:false。默认值:false |
| block_device_mapping_v2.destination_type | string | 否 | 定义卷从哪来的。有效值:local:临时磁盘位于服务器运行的计算主机的本地；volume:持久化卷存储在块存储服务中 |
| block_device_mapping_v2.device_name | string | 否 | 要用于引导云主机的卷的设备路径。注意，从12.0.0 Liberty版本开始，Nova libvirt驱动程序不再使用用户提供的设备名。这与请求中没有提供设备名参数是相同的行为。 |
| block_device_mapping_v2.device_type | string | 否 | 设备类型。例如:disk, cdrom。 |
| block_device_mapping_v2.disk_bus | string | 否 | 磁盘总线类型，一些虚拟化层(目前仅libvirt)支持指定此参数。例如，disk_bus的值可以是:fdc、ide、sata、scsi、usb、virtio、xen、lxc和uml。对每种总线类型的支持取决于虚拟化驱动程序和底层管理程序。 |
| block_device_mapping_v2.guest_format | string | 否 | 指定客户服务器磁盘的文件系统格式，如ext2、ext3、ext4、xfs或swap。<br/>交换块设备映射有以下限制:<br/>- source_type必须为空<br/>- destination_type必须是本地的<br/>- 每个服务器只能有一个交换磁盘<br/>- 交换盘的大小必须小于或等于flavor的交换盘大小 |
| block_device_mapping_v2.no_device | boolean | 否 | 当值为True时表示无设备。 |
| block_device_mapping_v2.source_type | string | 否 | 块设备的源类型。 有效值为：<br/>- blank：根据目标类型和来宾格式，这将是空白持久卷或服务器所在的计算主机本地的临时磁盘（或交换磁盘）<br/>- image：仅在destination_type = volume时有效； 在块存储服务中创建一个支持映像的卷并将其附加到服务器<br/>- snapshot：仅在destination_type = volume时有效； 创建由通过block_device_mapping_v2.uuid参数引用的给定卷快照支持的卷，并将其附加到服务器<br/>- volume：仅在destination_type = volume时有效； 使用通过block_device_mapping_v2.uuid参数引用的现有持久卷，并将其附加到服务器 |
| block_device_mapping_v2.uuid | string | 否 | 这是源资源的uuid。 uuid基于source_type指向不同的资源。 例如，如果source_type是image，则基于从图像服务检索的指定图像创建块设备。 同样，如果source_type是快照，则uuid引用块存储服务中的卷快照。 如果source_type是volume，则uuid引用块存储服务中的卷。 |
| block_device_mapping_v2.volume_size | integer | 否 | 卷的大小（以GiB为单位）。 这是范围从1到2147483647的整数值，可以整数和字符串的形式请求。 |
| block_device_mapping_v2.tag | string | 否 | 可以应用于块设备的设备角色标签。 具有以此方式标记的设备的服务器的来宾OS可以从元数据API和配置驱动器（如果已启用）访问有关标记的设备的硬件元数据。 |
| block_device_mapping_v2.volume_type | string | 否 | 设备的volume_type。这可用于指定计算服务将创建并连接到服务器的卷的类型。如果未指定，块存储服务将提供默认卷类型。有关详细信息，请参阅块存储卷类型API。 |
| imageRef | string | 否 | 用于创建云主机实例的镜像的UUID。在从卷引导的情况下，这不是必需的。在所有其他情况下，它都是必需的，并且必须是有效的UUID，否则API将返回400。 |
| key_name | string | 否 | 密钥对名称。 |
| metadata | object | 否 | 元数据键值对。metadata key和value的最大大小都是255字节。 |
| OS-DCF:diskConfig | string | 否 | 在创建、重新构建或调整服务器大小时，控制API如何对磁盘进行分区。服务器从创建它的映像继承OS-DCF:diskConfig值，映像从创建它的服务器继承OS-DCF:diskConfig值。若要重写继承的设置，可以在服务器创建、重新生成或调整请求的请求主体中包含此属性。如果镜像的OS-DCF:diskConfig值为MANUAL，则不能从该镜像创建服务器，并将其OS-DCF:diskConfig值设置为AUTO。有效值为:<br/>- AUTO：API用一个与目标flavor磁盘大小相同的分区构建服务器。API自动调整文件系统以适应整个分区。<br/>- MANUAL:API通过使用源映像中的任何分区方案和文件系统来构建服务器。如果目标flavor磁盘较大，API不会对剩余的磁盘空间进行分区。 |
| security_groups | array | 否 | 一个或多个安全组。在“名称”属性中指定安全组的名称。如果忽略此属性，API将在默认安全组中创建服务器。请求的安全组没有应用到已存在的端口。 |
| user_data | string | 否 | 启动时使用的配置信息或脚本。必须是Base64编码的。限制为65535字节。 |
| description | string | 否 | 服务器的自由形式描述。长度限制为255个字符。在microversion 2.19之前，这被设置为服务器名。<br/>2.19新版功能 |
| tags | string | 否 | 标签列表。标签有以下限制:<br/>- 标签是一个不超过60个字符的Unicode字节串。<br/>- Tag是一个非空字符串。<br/>- ' / '不允许出现在标签名称中<br/>- 为了简化指定标签列表的请求，在标签名称中不允许使用逗号<br/>- 所有其他字符都允许在标记名中<br/>- 每个服务器最多可以有50个标签。<br/>2.52新版功能 |
| host | string | 否 | 创建云主机的物理主机。 |
| hypervisor_hostname | string | 否 | 要在其上创建服务器的管理程序的主机名。如果没有找到具有给定主机名的虚拟机监控程序，API将返回400。缺省情况下，只能由管理员指定。 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.67"。

## 请求示例
示例一：创建云主机
```yaml
{
    "server" : {
        "accessIPv4": "1.2.3.4",
        "accessIPv6": "80fe::",
        "name" : "new-server-test",
        "imageRef" : "70a599e0-31e7-49b7-b260-868f441e862b",
        "flavorRef" : "1",
        "availability_zone": "us-west",
        "OS-DCF:diskConfig": "AUTO",
        "metadata" : {
            "My Server Name" : "Apache1"
        },
        "personality": [
            {
                "path": "/etc/banner.txt",
                "contents": "fake_contents"
            }
        ],
        "security_groups": [
            {
                "name": "default"
            }
        ],
        "user_data" : "fake_user_data"
    },
}
```

示例二：创建自动网络云主机（v2.37）
```yaml
{
    "server": {
        "name": "auto-allocate-network",
        "imageRef": "70a599e0-31e7-49b7-b260-868f441e862b",
        "flavorRef": "http://openstack.example.com/flavors/1",
        "networks": "auto"
    }
}
```


## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| server | object | 云主机对象。 |
| addresses | ojbect | 云主机地址。 |
| created | string | 云主机创建的日期和时间。 |
| flavor | string | 云主机使用的规格。 |
| hostid | string | 宿主机ID。 |
| id | string | 云主机ID。 |
| image | object | 创建云主机实例的镜像的UUID和链接信息。 |
| key_name | string | 密钥对名称。 |
| links | array | 只描述信息。 |
| metadata |  | 元数据键值对。metadata key和value的最大大小都是255字节。 |
| name | string | 云主机名称。   |
| accessIPv4 | string | 用于访问此服务器的IPv4地址。 |
| accessIPv6 | string | 用于访问此服务器的IPv6地址。 |
| OS-DCF:diskConfig | string | 在创建、重新构建或调整服务器大小时，控制API如何对磁盘进行分区。服务器从创建它的映像继承OS-DCF:diskConfig值，映像从创建它的服务器继承OS-DCF:diskConfig值。若要重写继承的设置，可以在服务器创建、重新生成或调整请求的请求主体中包含此属性。如果镜像的OS-DCF:diskConfig值为MANUAL，则不能从该镜像创建服务器，并将其OS-DCF:diskConfig值设置为AUTO。 |
| OS-EXT-AZ:availability_zone | string | 可用区域名称。 |
| OS-EXT-SRV-ATTR:host | string | 宿主机名字。 |
| OS-EXT-SRV-ATTR:hypervisor_hostname | string | 创建服务器的管理程序的主机名。 |
| OS-EXT-SRV-ATTR:instance_name | string | 云主机名字。 |
| OS-EXT-STS:power_state | integer | 云主机状态。 |
| OS-EXT-STS:task_state | string | 云主机工作状态。 |
| OS-EXT-STS:vm_state | string | 虚拟机运行状态。 |
| os-extended-volumes:volumes_attached | string | 挂载的云盘列表。 |
| OS-SRV-USG:launched_at | string | 云主机创建的日期和时间。 |
| OS-SRV-USG:terminated_at | string | 云主机删除的日期和时间。 |
| progress | integer | 云主机创建进度。 |
| security_groups | array | 一个或多个安全组。 |
| security_group.name | string | 安全组名称。 |
| status | string | 云主机状态。 |
| host_status | string | 宿主机状态。 |
| tenant_id | string | 云主机租户ID。 |
| updated | string | 云主机更新的日期和时间。 |
| user_id | string | 云主机用户ID。 |
| OS-EXT-SERV-ATTR:hostname | string | 云主机启动时的主机名。 |
| OS-EXT-SERV-ATTR:reservation_id | string | 云主机资源预留ID。 |
| OS-EXT-SERV-ATTR:launch_index | int | 同时创建多个虚拟机时的顺序。 |
| OS-EXT-SERV-ATTR:kernel_id | string | 使用AMI镜像时的内核镜像ID。 |
| OS-EXT-SERV-ATTR:ramdisk_id | string | 使用AMI镜像时的内存镜像ID。 |
| OS-EXT-SERV-ATTR:root_device_name | string | 云主机系统盘名称。 |
| OS-EXT-SERV-ATTR:user_data | string | 启动时使用的配置信息或脚本。必须是Base64编码的。限制为65535字节。 |
| estimated_deleted | string | 预计删除时间。 |


## 响应示例
```yaml
{
    "server": {
        "OS-DCF:diskConfig": "AUTO",
        "adminPass": "6NpUwoz2QDRN",
        "id": "f5dc173b-6804-445a-a6d8-c705dad5b5eb",
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
        "security_groups": [
            {
                "name": "default"
            }
        ]
    }
}
```


## 正常响应代码
202
# 启动云主机
## 功能介绍
启动停止的云主机并将其状态更改为“ACTIVE”。
## 前提条件

- 云主机状态必须为“SHUTOFF”。
## 故障排除

- 如果云主机状态不变为“ACTIVE”，则启动操作失败。 确保满足前提条件并再次运行请求。 如果请求再次失败，请调查是否正在运行另一个导致竞争条件的操作。
## 异步后置条件

- 成功启动云主机后，其状态将更改为“ACTIVE”。
## URI
`POST /v2.1/{project—id}/servers/{server_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_id | 是 | 云主机的UUID。 |


## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| os-start | string | 是 | 启动云主机的动作。 |


## 请求示例
```yaml
{
    "os-start" : true
}
```

## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 关闭云主机
## 功能介绍
关闭启动状态的云主机。
## 前提条件

- 云主机状态必须为“ACTIVE”。
## 异步后置条件

- 成功关闭云主机后，其状态将更改为“PAUSED”
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 虚拟机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| os-stop | string | 是 | 关闭云主机的动作。 |

## 请求示例
```yaml
{
    "os-stop" : true
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 重启云主机
## 功能介绍
重新启动云主机。
## URI
`POST /v2.1/{project—id}/servers/{server_id}/action`

| 参数 | 是否必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_id | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| reboot | object | 是 | 重启云主机的动作。 |
| type | string | 是 | 重启的类型，取值范围为['HARD', 'Hard', 'hard', 'SOFT', 'Soft', 'soft']
其中hard表示硬重启， soft表示软重启。 |

## 请求示例
```yaml
{
    "reboot": {
        "type": "SOFT"
    }
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 暂停云主机
## 功能介绍
暂停启动状态的云主机。
## 前提条件

- 云主机状态必须为“ACTIVE”。
## 异步后置条件

- 成功关闭云主机后，其状态将更改为“PAUSED”
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| pause | string | 是 | 暂停云主机的动作。 |

## 请求示例
```yaml
{
    "pause" : true
}
```
## 响应示例
POST操作成功的回复没有任何内容。

**正常响应代码**
202
# 恢复云主机
## 功能介绍
恢复暂停状态的云主机。
## 前提条件

- 云主机状态必须为“PAUSE”。
## 异步后置条件

- 成功恢复暂停状态的云主机后，其状态将更改为“ACTIVE”。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| unpause | string | 是 | 恢复云主机的动作。 |

## 请求示例
```yaml
{
    "unpause" : true
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 挂起云主机
## 功能介绍
挂起运行状态的云主机。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| suspend | string | 是 | 挂起云主机的动作。 |

## 请求示例
```yaml
{
    "suspend" : true
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 取消挂起云主机
## 功能介绍
恢复挂起的云主机并将其状态更改为“ACTIVE”。
## 前提条件

- 云主机状态必须为“SUSPENDED”。
## 异步后置条件

- 成功取消挂起状态的云主机后，其状态将更改为“ACTIVE”。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机的UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| resume | string | 是 | 取消挂起云主机的动作。 |

## 请求示例
```yaml
{
    "resume" : true
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 云主机编辑名称
## 功能介绍
编辑云主机名称。
## 异步后置条件

- 编辑云主机名称后，云主机名称为更新后的新名称。
## URI
`PUT /v2.1/{project_id}/servers/{server_uuid}`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 虚拟机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| server | object | 是 | 包含编辑云主机名称的对象。 |
| name | string | 是 | 用户自定义名称。 |

## 请求示例
```yaml
{
	"server": {
		"name": "instance-rename"
	}
}
```
## 响应示例
PUT操作成功的回复没有任何内容。
## 正常响应代码
200
# 云主机调整规格
## 功能介绍
调整云主机规格。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 虚拟机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| resize | object | 是 | 调整云主机规格的动作。 |
| flavorRef | string | 是 | 云主机规格ID。 |

## 请求示例
```yaml
{
	"resize": {
		"flavorRef": "214"
	}
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 创建快照
## 功能介绍
创建云主机快照。
## 前提条件

- 云主机状态可以为“ACTIVE”，“PAUSE”，“SUSPENDED”。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| createImage | object | 是 | 创建云主机快照的动作。 |
| metadata | dict | 否 | 云主机快照元数据。 |
| name | string | 是 | 云主机快照名字。 |

## 请求示例
```yaml
{
	"createImage": {
		"name": "zhz111-snapshot1",
		"metadata": {
			"description": ""
		}
	}
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 连接网络
## 功能介绍
为云主机连接一个新的网络。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/os-interface`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| interfaceAttachment | object | 是 | 要连接新的网络的数据对象。 |
| port_id | string | 否 | 要连接的网卡的id。 |
| net_id | string | 否 | 要连接的网络的id。 |
| fixed_ips  | array | 否 | 网卡的固定ip列表。 |
| ip_address | string | 否 | ip地址。 |

## 请求示例
```yaml
{
    "interfaceAttachment": {
        "port_id": "ce155147-9d3b-4c09-9079-da8de0d38df8"
    }
}
```
## 响应消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| interfaceAttachment | object | 是 | 要连接网络数据对象。 |
| port_id | string | 否 | 要连接的网卡的id。 |
| net_id | string | 否 | 要连接的网络的id。 |
| fixed_ips  | array | 否 | 网卡的固定ip列表。 |
| ip_address | string | 否 | ip地址。 |
| subnet_id | string | 否 | 子网的id。 |
| mac_addr | string | 否 | mac地址。 |
| port_state | string | 否 | 网卡的状态。 |

## 响应示例
```yaml
{
    "interfaceAttachment": {
        "fixed_ips": [
            {
                "ip_address": "192.168.1.3",
                "subnet_id": "f8a6e8f8-c2ec-497c-9f23-da9616de54ef"
            }
        ],
        "mac_addr": "fa:16:3e:4c:2c:30",
        "net_id": "3cb9bc59-5699-4588-a4b1-b87f96708bc6",
        "port_id": "ce531f90-199f-48c0-816c-13e38010b442",
        "port_state": "ACTIVE"
}
}
```
## 正常响应代码
200
# 断开网络
## 功能介绍
为云主机断开一个连接的网络。
## URI
`DELETE /v2.1/{project_id}/servers/{server_uuid}/os-interface/{port_id}`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |
| port_id | 是 | 要断开的网卡的id。 |


## 响应示例
成功请求后不返回任何body。
## 正常响应代码
202
# 挂载云硬盘
## 功能介绍
为云主机连接一个新的云硬盘。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/os-volume_attachments`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| volumeAttachment | object | 是 | 要挂载新的云硬盘的数据对象。 |
| volumeId | string | 是 | 要挂载的云硬盘的id。 |
| device | string | 否 | 要挂载的云硬盘的名字，例如/dev/vab。 |

## 请求示例
```yaml
{
    "volumeAttachment": {
        "volumeId": "a26887c6-c47b-4654-abb5-dfadf7d3f803",
        "device": "/dev/vdd"
    }
}
```
## 响应消息
| 参数 | 参数类型 | 描述 |
| --- | --- | --- |
| volumeAttachment | object | 要挂载的云硬盘的数据。 |
| device | string | 挂载给云主机设备的名称。 |
| id | string | 挂载信息的id。 |
| serverId | string | 云主机的id。 |
| volumeId | string | 云硬盘的id。 |

## 响应示例
```yaml
{
    "volumeAttachment": {
        "device": "/dev/vdd",
        "id": "a26887c6-c47b-4654-abb5-dfadf7d3f803",
        "serverId": "0c92f3f6-c253-4c9b-bd43-e880a8d2eb0a",
        "volumeId": "a26887c6-c47b-4654-abb5-dfadf7d3f803"
    }
}
```
## 正常响应代码
200
# 卸载云硬盘
## 功能介绍
为云主机卸载一个云硬盘。
## URI
`DELETE /v2.1/{project_id}/servers/{server_uuid}/os-volume_attachments/{attachment_id}`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |
| attachment_id | 是 | 挂载云硬盘的id。 |

## 响应示例
成功请求后不返回任何body。
## 正常响应代码
202
# 冷迁移
## 功能介绍
把虚拟机迁移到其它主机上
## URI
`POST /servers/{server_id}/action`
## 请求消息
| 名称 | 参数类型 | 描述 |
| --- | --- | --- |
| server_id | string | 虚拟机的uuid |
| migrate | object | 迁移对象 |
| host(可选) | string | 目标主机 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.56"。

## 请求示例
```yaml
{
    "migrate":{
        "host":"node-1.domain.tld"
    }
}
```
## 响应消息
无
## 正常响应代码
202
# 热迁移
## 功能介绍
把虚拟机热迁移到其它主机
## URI
`POST /servers/{server_id}/action`
## 请求消息
| 名称 | 参数类型 | 描述 |
| --- | --- | --- |
| os-migrateLive | object | 热迁移对象。 |
| server_id | string | 虚拟机的uuid |
| host | string | 目的主机名称 |
| block_migration | boolean | 块迁移，2.24版本前是布尔型 |
| block_migration | string | 块迁移，2.25版本开始是字符串型 |
| dislk_over_commit | boolean | 磁盘超配 |
| force(可选) | boolean | 指定了目标节点是否强制热迁移 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.25"。

## 请求示例
```yaml
{
    "os-migrateLive":{
        "block_migration":"auto",
        "host":"node-2.domain.tld"
    }
}
```
## 响应消息
无
## 正常响应代码
202
# 撤离
## 功能介绍
把虚拟机从故障主机撤离
## URI
POST /servers/{server_id}/action
## 请求消息
| 名称 | 参数类型 | 描述 |
| --- | --- | --- |
| server_id | string | 虚拟机uuid |
| evacuate | string | 撤离对象 |
| host(可选) | string | 目的主机 |
| adminPass(可选) | string | 管理密码 |
| onSharedStorage | boolean | 共享存储 |
| force(可选) | boolean | 选定目的主机强制撤离 |

注：建议您在请求头中设置如下内容以使用推荐版本的API："X-OpenStack-Nova-API-Version: 2.25"。

## 请求示例
```yaml
{
    "evacuate":{
    }
}
```
## 响应消息
| 名称 | 参数类型 | 描述 |
| --- | --- | --- |
| adminPass(可选) | string | 管理密码 |

## 正常响应代码
200
# 重置云主机状态
## 功能介绍
重置云主机的状态。
## 接口约束
策略默认值仅允许具有管理角色执行此操作。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| os-resetState | string | 是 | 重置云主机状态的动作。 |
| os-resetState.state | string | 是 | 重置云主机的状态，active或者error。 |

## 请求示例
```yaml
{
    "os-resetState": {
        "state": "active"
    }
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 锁定云主机
## 功能介绍
锁定云主机。
## 接口约束
策略默认值仅允许具有管理角色或云主机所有者的用户执行此操作。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息

| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| lock | string | 是 | 锁定云主机的动作。 |

## 请求示例
```yaml
{
    "lock": null
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 解锁云主机
## 功能介绍
解锁锁定的云主机。
## 接口约束
策略默认值仅允许具有管理角色或云主机所有者的用户执行此操作。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| unlock | string | 是 | 解锁锁定云主机的动作。 |

## 请求示例
```yaml
{
    "unlock": null
}
```
## 响应示例
POST操作成功的回复没有任何内容。
## 正常响应代码
202
# 重建云主机
## 功能介绍
重建云主机。
## URI
`POST /v2.1/{project_id}/servers/{server_uuid}/action`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求消息
| 参数 | 参数类型 | 是否必选 | 描述 |
| --- | --- | --- | --- |
| rebuild | object | 是 | 重建云主机的动作。 |
| imageRef | string | 是 | 重建要使用的镜像ID。 |
| name | string | 否 | 重建的云主机名称。 |
| adminPass | string | 否 | 重建云主机的管理员密码。 |
| metadata | object | 否 | 重建云主机要使用的元数据。 |

## 请求示例
```yaml
{
    "rebuild" : {
        "imageRef" : "70a599e0-31e7-49b7-b260-868f441e862b",
        "name" : "foobar",
        "adminPass" : "seekr3t",
        "metadata" : {
            "meta_var" : "meta_val"
        }
    }
}
```
## 正常响应代码
202
# 删除云主机
## 功能介绍
移动云主机到回收站。
## URI
`DELETE /v2.1/{project—id}/servers/{server_id}`

| 参数 | 是否action必选 | 描述 |
| --- | --- | --- |
| project_id | 是 | 项目ID。 |
| server_uuid | 是 | 云主机UUID。 |

## 请求示例
`DELETE /v2.1/87aca7a4e69d4da09a3de67c28f3d48d/servers/89b37e3e-592a-4626-a2d4-aa48219b3323`
## 响应消息
对DELETE操作成功的响应没有任何内容。
## 正常响应代码
204