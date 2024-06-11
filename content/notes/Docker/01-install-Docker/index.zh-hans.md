---
title: 安装 Docker 引擎
description: "VMware 虚拟 CentOS 7系统安装 Docker 引擎。"
# linkTitle:
date: 2024-04-09T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 1
nav_icon:
  vendor: bootstrap
  name: grid-3x3
  color: RoyalBlue
series:
  - Docker
categories:
  - 笔记
tags:
  - Docker
  - 安装
  - Linux
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

# 安装Docker引擎


## 安装环境

* VMware 虚拟 CentOS 7系统
* 使用Xshell 远程连接服务器

    CentOS 7防火墙开启22端口
```

	firewall-cmd --zone=public --permanent --add-port=22/tcp
	
```

## 参考学习内容

* [【docs.docker】官网文档](https://docs.docker.com/engine/install/centos/)Install Docker Engine on CentOS
* [【狂神说Java】Docker最新超详细版教程通俗易懂](https://www.bilibili.com/video/BV1og4y1q7M4)

## 具体步骤

* 1、卸载旧版本的 Docker，以及关联的依赖项。
```
        yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

```
* 2、安装工具软件包。
```
	yum install -y yum-utils
```
* 3、设置镜像的仓库

官网说明是以下命令：
```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  # 默认使用国外的
```

根据狂神的教程视频里推荐使用国内阿里云：
```
yum-config-manager \
--add-repo \
http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo # 推荐使用阿里云的，十分的快
```

* 4、狂神建议：更新 yum 软件包索引
```
yum makecache fast
```


* 5、安装 Docker Engine、containerd 和 Docker Compose

其中 docker-ce 是社区版；另外，ee是企业版，
```
yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
* 6、启动 Docker。
```
	systemctl start docker
```
* 7、通过运行映像来验证 Docker 引擎安装是否成功。
```
	docker run hello-world
```

运行后，显示文字包括如下内容，即表示安装成功
```
	Status: Downloaded newer image for hello-world:latest

	Hello from Docker!
	This message shows that your installation appears to be working correctly.
```


* 8、查看下载的 hello-world 镜像

```
docker images
```

* 9、了解一下：卸载 docker 引擎

卸载 Docker Engine、CLI、containerd 和 Docker Compose 包：
```
sudo yum remove docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

主机上的映像、容器、卷或自定义配置文件不会自动删除。要删除所有映像、容器和卷，请执行以下操作：
```
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```
您必须手动删除任何已编辑的配置文件。
