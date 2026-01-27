---
title: CentOS镜像创建的云主机重启后主机名变化，如何排查解决
---
# 问题描述

基于CentOS镜像创建的云主机，在第一次启动后会获取到一个主机名，但是，在重启后该主机名发生变化，其后会加上novalocal的后缀。

# 问题原因

由于CentOS镜像中安装有cloud-init服务，导致该服务的缺陷问题被引入。

# 解决方案

1. 在该云主机的控制台中，通过VIM编辑器，打开cloud-init文件。具体命令如下:

       vim /usr/lib/python2.6/site-packages/cloudinit/distros/__init__.py

2. 将87行的 **write_hostname** 修改为 **hostname** 。

