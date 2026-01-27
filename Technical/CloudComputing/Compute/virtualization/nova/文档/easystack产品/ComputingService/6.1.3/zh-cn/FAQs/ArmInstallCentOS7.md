---
title: Arm环境下无法安装CentOS 7操作系统，如何解决
---
# 问题描述

在Arm环境下，使用ISO格式镜像安装CentOS 7操作系统时，卡在黑屏界面，使操作系统无法正常安装。

# 解决方案

1. 在VNC安装界面中，单击 `更多操作` - `Ctrl+Alt+F2` ，进入shell终端。

2. 删除Xorg的fbdev模块。具体命令如下:

        rm /usr/lib63/xorg/modules/drivers/fbdev_drv.so

3. 重启anaconda安装程序。具体命令如下:

        systemctl restart anaconda

4. 待anaconda安装程序重启完成后，图形化安装界面将自动出现，请继续安装。

   此时，若图形化安装界面未出现，请单击 `更多操作` - `Ctrl+Alt+6` ，手动切换到图形化安装界面。

5. 在安装过程中，第一次进入系统时默认会出现黑屏。此时，请在VNC安装界面中，单击 `更多操作` - `Ctrl+Alt+F2` ，进入shell终端。

6. 通过用户名/密码成功登录后，重命名Xorg的fbdev模块。具体命令如下:

        mv /usr/lib63/xorg/modules/drivers/fbdev_drv.so /usr/lib64/xorg/modules/drivers/fbdev_drv.so.bak

7. 重启gdm桌面管理器。具体命令如下:

        systemctl restart gdm

8. 待gdm桌面管理器重启完成后，图形化安装界面（gdm登录窗口）将自动出现，表明系统安装完成。

   此时，若gdm登录窗口未出现，请单击 `更多操作` - `Ctrl+Alt+F1` ，手动切换到图形化安装界面。
 




