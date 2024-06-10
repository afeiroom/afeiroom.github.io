---
title: 在 Linux 下使用 Clash for Windows GUI
description: "在 Linux 上推荐使用 Clash for Windows 的 GUI 版本。"
# linkTitle:
date: 2024-04-14T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 1
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
  - Clash
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

# 在 Linux 下使用 Clash for Windows GUI
Clash 是一款基于规则的多平台代理工具，支持 Windows、macOS、Linux、Android、iOS 等多个平台。在 Linux 上推荐使用 Clash for Windows 的 GUI 版本。

  　　————2024.4.14

## 下载

* [镜像1](https://dl.gtk.pw/proxy/linux)
* [镜像2](https://down.gtk.pw/proxy/linux)
* [Box 镜像3](https://app.box.com/s/my3vtk7cxefp7v69vsnzg3kebehqba1x/folder/211969947230)
* [Dropbox 镜像4](https://www.dropbox.com/scl/fo/u7wj2midvatkxxvoik9yz/h?dl=0&rlkey=wqgf774hnk88sginx05c9agkh)

## 使用
由于 Linux 发行版本比较多，这里无法对每一个发行版做介绍，下面以 CentOS7 下使用为例。

首先根据上方的链接获取安装包。

解压缩，注意将具体的文件名字替换为自己下载的文件名。
```
tar -xvf clash-linux-amd64-*.gz
```

在解压出来的文件夹中找到 cfw 这个可执行文件。

然后在终端中进入该文件夹，执行 `./cfw` 即可启动 Clash for Windows 的 GUI 版本。

本机执行 `./cfw` 之后系统提示：`Running as root without --no-sandbox is not supported.`

增加 `--no-sandbox` 参数后执行成功。

```
./cfw --no-sandbox
```

## 配置
注册并使用**机场**服务 并获取配置链接。

在自己的**机场**服务商的页面**复制 Clash 订阅链接**。

然后回到 Clash for Windows 页面，在界面中点击左侧的 Profiles，然后在右侧的输入框中输入配置链接，点击 Download 即可。

![ClashDownload.png](https://s2.loli.net/2024/06/10/OHPACwtz59GQVip.png)

订阅成功之后会在下方产生一个配置，点击配置，选中。

然后再点击左侧 Proxies，选择需要使用的代理，点击 Apply 即可。

## 在 Linux 中设置系统代理
由于 Clash for Windows 的系统代理功能只在 Windows 和 macOS 下生效，所以在 Linux 下需要手动设置系统代理。

在系统设置中，找到网络代理设置。

![ClashProxy.png](https://s2.loli.net/2024/06/10/SVznNtXKocAxm5g.png)

设置网络代理。

![ClashsetProxy.png](https://s2.loli.net/2024/06/10/41PgxHZeLEc9J7I.png)

完成设置后，即可使用代理。