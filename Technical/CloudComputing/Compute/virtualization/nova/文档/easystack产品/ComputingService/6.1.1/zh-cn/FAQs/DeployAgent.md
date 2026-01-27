---
title: 如何安装重置密码插件（Agent）
---
# 问题描述

云平台为云主机提供重置密码功能，用于在密码丢失、密码遗忘或密码过期等场景下，重置Windows系统云主机中Administrator用户的密码或Linux系统云主机中root用户的密码。但是，该功能的正常使用依赖于Agent插件的正确安装。所以，当已确定在创建云主机时所用镜像已正确安装该插件，则可直接使用重置密码功能。否则，必须先在云主机内检查或安装此插件。

> 说明：
>
> * 该Agen插件，除可用于为云主机提供重置密码功能外，还支持为云主机提供详细监控功能。
> * 在制作云主机镜像时，如需安装或配置云主机Agent，也可参考以下内容进行操作。

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

1. 远程登录云主机，安装名称前缀为 **qemu-ga** 的Agent插件安装包。

2. 打开命令提示符（CMD），输入“Services.msc”，打开“服务”窗口。

3. 在“服务”窗口，启动插件服务（名称前缀为 **QEMU Guest Agent** 的两个服务）。