---
title: 如何安装QEMU Guest Agent
---
# 问题描述

qemu-guest-agent(以下简称为qga)是运行在客户机操作系统中的一个守护进程，该守护进程和宿主机上的QEMU配合，可在宿主机和客户机之间打开一个相互交换信息的数据通道，以强化Hypervisor对客户机的管理能力。例如安装qga后，客户机中能执行宿主机发出的特定命令，从而增强客户机的自动化能力。当前，客户机中的qga服务与云平台控制面相结合可执行以下任务：
* 响应重置密码的请求，修改客户机管理员的登录密码。
* 定期从客户机收集CPU、内存、磁盘、网络使用情况信息。

所以如果要云主机能够支持重置密码的功能和从云主机内部获取系统运行状态的功能（云主机详细监控功能），则必须保证云主机中已正确安装并启用qga。可以在制作云主机镜像时安装qga，也可以在云主机启动好后再手动安装qga，具体安装方法如下：


# 解决方案

请根据实际云主机操作系统的类型，酌情选择下述对应操作步骤安装Agent插件。

## 针对Linux操作系统的云主机（以CentOS 7为例）

1. 远程登录云主机，并确认系统未安装Agent插件。具体命令如下:

         yum list | grep qemu-guest-agent

   当查询结果为空时，则代表未安装此插件。否则，则代表已安装此插件。

2. （可选）当确认未安装Agent插件时，则必须执行此操作。否则，可直接跳过本步骤。
   
   1. 安装Agent插件。具体命令如下:

           yum install qemu-guest-agent -y

   2. 待安装完成后，请查看 **/etc/sysconfig/qemu-ga** 文件，确认 **BLACKLIST_RPC** 中不包含以下字段：guest-exec、guest-exec-status、guest-network-get-interfaces和guest-get-osinfo。当该文件中含有上述任一字段时，请将其直接删除。

3. 确认插件服务为开机启动。具体命令如下:

         systemctl list-unit-files | grep enable |grep qemu

   当查询结果显示 **qemu-guest-agent** 时，则代表插件服务为开机启动。否则，请执行以下命令，设置其为开机启动: 

         systemctl enable --now qemu-guest-agent

4. 确认插件服务为运行状态。具体命令如下:

         systemctl status qemu-guest-agent.service

   当查询结果显示 **Active** 时，则代表插件服务为运行状态。否则，请执行以下命令，设置其为运行状态:

         systemctl restart qemu-guest-agent.service

## 针对Windows操作系统的云主机

1. 下载virtio-win driver镜像文件。

   镜像文件下载地址为：[Download Windows VirtIO Drivers](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso)。

2. 安装virtio-serial driver。

   1. 挂载下载的ISO（virtio-*.iso）到Windows云主机。

   2. 打开Windows设备管理器，找到“PCI Simple Communications Controller”，右击并选择更新驱动。

   3. 更新驱动时选择挂载的ISO上的目录：DRIVE:\vioserial\<OSVERSION>\ 。其中，<OSVERSION>请输入当前云主机的Windows版本 (例如：Windows 2012 R2需输入2k12R2)。

3. 安装qga。

   1. 在挂载的ISO中进入qga的安装文件所在目录（即：guest-agent）。

   2. 双击执行qga的安装文件（qemu-ga-x86_64.msi (64-bit) 或 qemu-ga-i386.msi (32-bit)）。

4. 确认qga已正常运行。

   在Windows Services列表中或在PowerShell中执行以下命令进行验证:

         Get-Service QEMU-GA

   * 当qga运行正常时，显示结果如下:

         Status   Name               DisplayName
         ------   ----               -----------
         Running  QEMU-GA            QEMU Guest Agent

   * 当qga运行异常时，请在Services控制面板中对其执行重新启动操作。此外，请确保已设置该服务随系统启动运行。