---
title: CentOS 7系统安装图形界面
description: "如何切换到图形化界面模式去应用？"
# linkTitle:
date: 2024-04-25T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 4
nav_icon:
  vendor: bootstrap
  name: ubuntu
  color: OrangeRed
series:
  - Linux
categories:
  - 笔记
tags:
  - Linux
  - CentOS 7
  - 图形化
images:
#  - https://s2.loli.net/2024/06/09/rmpsa3cxeOgutIo.jpg?width=1920&height=1440
# menu:
#   main:
#     weight: 100
#     params:
#       icon:
#         vendor: bs
#         name: book
#         color: '#e24d0e'
authors:
  - Afei
---

# CentOS 7系统安装图形界面

	
在VMware虚拟机中成功安装CentOS 7系统后，如果启动CentOS 7系统直接进入命令行模式，没有进入操作系统桌面模式，那么应该是没有配置安装GUI图形界面的程序包所致，启动系统会默认进入命令行模式的界面。

如果首次使用，不习惯命令行的模式，如何切换到图形化界面模式去应用？

针对上述问题，其实CentOS 7可以将命令行模式转换为图形化界面模式启动，只需要联网状态下下载CentOS 7系统所需的GUI模式的程序包进行安装和配置即可。

## 参考资料

[黑马程序员【CentOS 7系统启动后怎么从命令行模式切换到图形界面模式】](https://zhuanlan.zhihu.com/p/126601630)

## 核心步骤

* 首次安装后，启动centOS 7系统，通过root用户登录命令行
* 查看CentOS 7 的默认启动模式（命令行模式显示：multi-user.target）
* 修改CentOS 7 的默认启动模式（图形化界面显示：graphical.target）
* 配置CentOS 7 系统的网卡信息，实现虚拟机与外网保持联通
* 通过yum命令获取并且安装图形界面GNOME的程序包
* 安装成功后，重启CentOS 7 系统，检验GUI界面效果

## 实现过程

1. 查看CentOS 7 的默认启动模式：`systemctl get-default`
~~~
[root@192 ~]# systemctl get-default
multi-user.target		# 命令行启动模式
~~~

2. 查看CentOS 7系统支持的启动模式

查看配置文件 `cat /etc/inittab`
~~~
[root@192 ~]# cat /etc/inittab
# inittab is no longer used when using systemd.
#
# ADDING CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.
#
# Ctrl-Alt-Delete is handled by /usr/lib/systemd/system/ctrl-alt-del.target
#
# systemd uses 'targets' instead of runlevels. By default, there are two main targets:
#
# multi-user.target: analogous to runlevel 3		# 支持命令行界面
# graphical.target: analogous to runlevel 5		# 支持图形化界面
#
# To view current default target, run:
# systemctl get-default
#
# To set a default target, run:
# systemctl set-default TARGET.target
#
~~~

3. 设置的centOS 7系统默认启动模式：
~~~
[root@192 ~]# systemctl set-default graphical.target
Removed symlink /etc/systemd/system/default.target.
Created symlink from /etc/systemd/system/default.target to /usr/lib/systemd/system/graphical.target.
~~~
设置为图形化界面模式：`systemctl set-default graphical.target`
设置为命令行界面模式：`systemctl set-default multi-user.target`


查看CentOS 7 修改后的默认启动模式：
~~~
[root@192 ~]# systemctl get-default
graphical.target		# 图形化界面启动模式
~~~



4. 配置网卡信息，使得虚拟机能够连通外网
~~~
#进入系统网卡配置文件
cd /etc/sysconfig/network-scripts/
#找到ifcfg-ens33文件，进行编辑
vi ifcfg-ens33
#修改启动设备参数为yes
ONBOOT=yes
#增加DNS配置信息
DNS1=8.8.8.8
DNS2=4.2.2.2
#编辑后保存退出
:wq
~~~
详见【CentOS 7 网络配置】

5. 通过yum命令获取并且安装图形界面GNOME的程序包

检查yum命令是否支持
~~~
[root@192 ~]# yum -h
已加载插件：fastestmirror, langpacks
Usage: yum [options] COMMAND

List of Commands:

check          检查 RPM 数据库问题
check-update   检查是否有可用的软件包更新
clean          删除缓存数据
……
  --sec-severity=SEVS, --secseverity=SEVS
                        Include security relevant packages matching the
                        severity, in updates

  插件选项:
[root@192 ~]# 
~~~

通过yum命令获取资源并安装图形化界面包，直到complete！
`yum groupinstall "GNOME Desktop" "Graphical Administration Tools"`
```
[root@192 ~]# yum groupinstall "GNOME Desktop" "Graphical Administration Tools"
已加载插件：fastestmirror
没有安装组信息文件
Maybe run: yum groups mark convert (see man yum)
Determining fastest mirrors
 * base: mirrors.nju.edu.cn
 * extras: mirrors.nju.edu.cn
 * updates: mirrors.nju.edu.cn
base                                        | 3.6 kB     00:00     
extras                                      | 2.9 kB     00:00     
updates                                     | 2.9 kB     00:00     
警告：分组 core 不包含任何可安装软件包。
警告：分组 graphical-admin-tools 不包含任何可安装软件包。
……
……
……
作为依赖被升级:
  kpartx.x86_64 0:0.4.9-136.el7_9              krb5-libs.x86_64 0:1.15.1-55.el7_9       nspr.x86_64 0:4.35.0-1.el7_9                   
  nss.x86_64 0:3.90.0-2.el7_9                  nss-softokn.x86_64 0:3.90.0-6.el7_9      nss-softokn-freebl.x86_64 0:3.90.0-6.el7_9     
  nss-sysinit.x86_64 0:3.90.0-2.el7_9          nss-tools.x86_64 0:3.90.0-2.el7_9        nss-util.x86_64 0:3.90.0-1.el7_9               
  open-vm-tools.x86_64 0:11.0.5-3.el7_9.9      systemd.x86_64 0:219-78.el7_9.9          systemd-libs.x86_64 0:219-78.el7_9.9           
  systemd-sysv.x86_64 0:219-78.el7_9.9        

完毕！
[root@192 ~]# 
```

6. 检查默认启动方式，重启centOS 7

查看默认启动方式是否是图形化界面：`systemctl get-default`

重启centOS 7：`reboot`

7. 登录成功进入桌面系统界面

可根据自己需要设置系统语言