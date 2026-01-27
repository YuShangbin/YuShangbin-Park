---
title: 使用限制
---

* 针对SR-IOV网卡：

   * 启用SR-IOV网卡的云主机不支持外部网络、安全组、QoS、VxLAN和云主机热迁移功能。

   * 在Arm架构的云平台中，飞腾不支持SR-IOV功能。鲲鹏支持SR-IOV功能，但是不支持挂起/恢复云主机，若因挂起导致云主机状态错误，请重置云主机状态，然后执行强制重启操作。

   * Intel的SR-IOV网卡支持的Windows操作系统版本包括Windows Server 2019\*、Windows Server 2016\*、Windows Server 2012\*以及Windows Server 2012\* R2，为了在Windows系统的云主机中使用SR-IOV功能，您需要选择以上受支持版本的镜像，并安装相应版本的驱动程序。

   * 删除启用SR-IOV网卡的云主机后，SR-IOV虚拟网卡将自动释放，但是不会被回收，可以手动删除或者绑定到其他云主机使用。

   * 当云平台从V5升级至V6版本时，无论SR-IOV网卡是在升级前已插入还是升级后新插入，若需使用SR-IOV功能均请申请变更单，具体变更内容请参见运维手册中相关内容。

     当全新安装V6版本的云平台时，若在安装前已插入SR-IOV网卡，则可直接使用；若需要在安装后插入SR-IOV网卡，则请先将该操作节点置于维护模式并关机，待插入SR-IOV网卡后，再启动该节点，并申请变更单将网卡变更为UP状态。

* 针对GPU：

   * 在Arm架构的云平台中，不支持使用GPU功能。

   * 请确保物理机BIOS中已开启Intel VT-d / AMD IOMMU功能，且物理机内核已开启IOMMU支持。

   * 当使用NVIDIA vGPU时，请先参考NVIDIA官方文档提前购买许可，搭建License Server并导入许可。此外，NVIDIA vGPU功能依赖CentOS 7.6版本内核，请使用c76版本ISO。

   * 目前云平台支持的GPU型号如下表所示，下述所列GPU均可用于GPU透传和虚拟化切割。支持对公网IP类型的资源计费。


<table>
<thead>
    <tr>
      <th>类型</th>
      <th>型号</th>
    </tr>
</thead>
<tbody>
    <tr>
        <td rowspan="11">NVIDIA</td>
        <td>Tesla V100</td>
    </tr>
    <tr>
        <td>Tesla P100</td>
    </tr>
    <tr>
        <td>Tesla P40</td>
    </tr>
    <tr>
        <td>Tesla P6</td>
    </tr>
    <tr>
        <td>Tesla P4</td>
    </tr>
    <tr>
        <td>Tesla M60</td>
    </tr>
    <tr>
        <td>Tesla M10</td>
    </tr>
    <tr>
        <td>Tesla M6</td>
    </tr>
    <tr>
        <td>Tesla T4</td>
    </tr>
    <tr>
        <td>Quadro RTX 8000</td>
    </tr>
    <tr>
        <td>Quadro RTX 6000</td>
    </tr>
    <tr>
        <td>Cambricon</td>
        <td>MLU100</td>
    </tr>
</tbody></table>