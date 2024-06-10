---
title: CentOS7下载安装 Golang
description: "官网下载 .tar.gz 手动安装，并设置环境变量。"
# linkTitle:
date: 2024-04-27T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 7
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
  - Golang
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

# CentOS7下载安装Golang


## 参考资料

[瘦身小蚂蚁【Centos7 安装 Go 及 Go版本升级】](https://blog.csdn.net/ling1998/article/details/120928614)

[disabled_csdN【centos7安装golang最新版1.22.2】](https://blog.csdn.net/qq_33997198/article/details/118333272)

## 1. 下载Go

官网地址：https://golang.google.cn/dl/
到官网查询2024年4月，最新版本已更新至1.22.2，Linux版本下载地址 https://golang.google.cn/dl/go1.22.2.linux-amd64.tar.gz
使用以下命令下载：
`wget https://golang.google.cn/dl/go1.22.2.linux-amd64.tar.gz`

```
[root@192 ~]# wget https://golang.google.cn/dl/go1.22.2.linux-amd64.tar.gz
--2024-04-27 12:19:35--  https://golang.google.cn/dl/go1.22.2.linux-amd64.tar.gz
正在解析主机 golang.google.cn (golang.google.cn)... 114.250.67.34
正在连接 golang.google.cn (golang.google.cn)|114.250.67.34|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 302 Found
位置：https://dl.google.com/go/go1.22.2.linux-amd64.tar.gz [跟随至新的 URL]
--2024-04-27 12:19:36--  https://dl.google.com/go/go1.22.2.linux-amd64.tar.gz
正在解析主机 dl.google.com (dl.google.com)... 114.250.67.33
正在连接 dl.google.com (dl.google.com)|114.250.67.33|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：68958123 (66M) [application/x-gzip]
正在保存至: “go1.22.2.linux-amd64.tar.gz”

100%[==============================================================================>] 68,958,123  47.5MB/s 用时 1.4s

2024-04-27 12:19:38 (47.5 MB/s) - 已保存 “go1.22.2.linux-amd64.tar.gz” [68958123/68958123])

```

若提示 ~bash: wget: commond not found，则安装wget
`yum install -y wget`

## 2. 解压压缩包
```
tar 参数：-C<目的目录>或--directory=<目的目录> 切换到指定的目录。
```

使用 `tar -C /usr/local -xzf go1.22.2.linux-amd64.tar.gz` 命令：
```
[root@192 ~]# tar -C /usr/local/ -xzf go1.22.2.linux-amd64.tar.gz
[root@192 ~]#
```

## 3. 配置环境变量
`vi /etc/profile`
```
[root@192 ~]# vi /etc/profile
```
    在 /etc/profile 文件最后添加下面配置
```
export GO111MODULE=on
export GOROOT=/usr/local/go 
export GOPATH=/home/gopath
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
     创建/home/gopath目录

`mkdir /home/gopath`
```
[root@192 ~]# mkdir /home/gopath
```
## 4. 重新读取配置

`source /etc/profile`
```
[root@192 ~]# source /etc/profile
```
## 5. 查看版本信息
`go version`

```
[root@192 ~]# go version
go version go1.22.2 linux/amd64
```
输出版本信息，则安装成功！
