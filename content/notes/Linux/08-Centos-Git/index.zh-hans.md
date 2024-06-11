---
title: CentOS7安装 Git
description: "yum 命令安装，此方法简单，并且会自动安装依赖的包，不过不一定是最新版的 git。"
# linkTitle:
date: 2024-04-27T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 8
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
  - Git
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

# CentOS7安装Git

	
yum命令安装：

`sudo yum install -y git`

```
[root@192 ~]# yum install git
已加载插件：fastestmirror, langpacks
……
已安装:
  git.x86_64 0:1.8.3.1-25.el7_9

作为依赖被安装:
  perl-Error.noarch 1:0.17020-2.el7     perl-Git.noarch 0:1.8.3.1-25.el7_9     perl-TermReadKey.x86_64 0:2.30-20.el7

完毕！
```
此方法简单，并且会自动安装依赖的包，而且会从源里安装最新的版本（不过不一定是最新的git）。

