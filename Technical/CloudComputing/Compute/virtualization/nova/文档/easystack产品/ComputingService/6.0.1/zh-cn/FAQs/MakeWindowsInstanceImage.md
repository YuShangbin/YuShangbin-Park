---
title: 如何制作Windows云主机镜像
---
# 问题描述

当创建Windows云主机时，若选择“镜像”作为启动源，则需要根据客户实际业务需求，提前制作云平台可用的Windows镜像。

# 解决方案

1. 使用virt-manager，挂载操作系统ISO和virtio-win。其中，在识别到硬盘后，不要进行分区，请直接安装系统。

   当制作Windows 2008的镜像时，识别磁盘需要使用virtio-win-0.1-81.iso，安装网卡驱动需要选择virtio-win-0.1-102.iso。获取链接如下：[获取virtio-win-0.1-81.iso](https://fedorapeople.org/groups/virt/virtio-win/deprecated-isos/stable/) 、[获取virtio-win-0.1-102.iso](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.102/)。

2. 待系统安装完成后，安装ballon，并将 virtio-win-0.1-XXX.iso 内容拷贝一份至本地。

3. 在Cloudbase的官网下载对应64或32位的Cloudbase-init，并进行安装。

   安装成功后，部分版本会提示可选择自动进行一次sysprep，将Windows系统重置，在下一次启动时进行重新的初始化。当没有提示时，也可自行进行sysprep操作。

4. （可选）针对Windows Server 2008 R2镜像创建的云主机，其系统时间会比宿主机操作系统时间少8个小时，请使用以下方法解决：

   * 针对已完成创建的Windows云主机，请在云主机内做如下修改：

     1. 在“运行中”输入 “regedit”，打开注册表。

     2. 依次展开HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Control/TimeZoneInformation后，新增名为“RealTimeIsUniversal”的项。该项的类型请选择“DWORD”，值请输入“ 1”。 

     3. 重启云主机，以使修改生效。

   * 针对Windows Server 2008 R2镜像，请更新镜像文件内容。具体命令如下:
   
          glance image-update <windows-imageuuid> —property os_type='windows'