---
title: Docker的常用命令
description: "Docker的常用命令。"
# linkTitle:
date: 2024-04-16T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 2
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
  - 常用命令
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

# Docker的常用命令

	
## 帮助命令

```
docker version		# 显示docker的版本信息 
docker info		# 显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help	# 万能命令
```

Docker 帮助文档的地址：https://docs.docker.com/reference/

## 镜像命令

### docker images
默认值将显示所有顶级镜像、它们的存储库和标签，以及它们的大小。`docker images`

#### 选项
| 参数         | 描述                                                                                                                                                                                                                                                                                                            |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -a, --all    | 显示所有镜像（默认隐藏中间镜像）                                                                                                                                                                                                                                                                                |
| --digests    | 显示摘要                                                                                                                                                                                                                                                                                                        |
| -f, --filter | 根据提供的条件筛选输出                                                                                                                                                                                                                                                                                          |
| --format     | 使用自定义模板设置输出格式：<br />“table”：使用列标题以表格格式打印输出（默认）<br />“table TEMPLATE”：使用给定的 Go 模板以表格格式打印输出<br />“json”：以 JSON 格式打印<br />“TEMPLATE”：使用给定的 Go 模板打印输出。<br />参考https://docs.docker.com/go/formatting/<br />有关使用模板设置输出格式的详细信息 |
| --no-trunc   | 不要截断输出                                                                                                                                                                                                                                                                                                    |
| -q, --quiet  | 仅显示图像 ID                                                                                                                                                                                                                                                                                                   |
```
[root@localhost ~]# docker images
REPOSITORY    TAG                  IMAGE ID       CREATED         SIZE
python        3.11-slim-bullseye   f5e43f6dcc5a   12 days ago     128MB
python        3.9-bullseye         845340d6d07d   3 weeks ago     906MB
hello-world   latest               d2c94e258dcb   11 months ago   13.3kB

# 解释
REPOSITORY      镜像的仓库源
TAG		镜像的标签
IMAGE ID	镜像的id
CREATED		镜像的创建时间
SIZE		镜像的大小

# 可选项
  -a, --all             # 显示所有镜像（默认隐藏中间镜像）
  -q, --quiet           # 只显示镜像的id

```

### docker search

描述	在 Docker Hub 中搜索镜像
用法	`docker search [OPTIONS] TERM`

#### 选项
| 参数         | 描述                           |
| ------------ | ------------------------------ |
| -f, --filter | 根据提供的条件筛选输出         |
| --format     | 使用 Go 模板进行漂亮的打印搜索 |
| --limit      | 最大搜索结果数                 |
| --no-trunc   | 不要截断输出                   |

```
[root@localhost ~]# docker search mysql
NAME                            DESCRIPTION                                      STARS     OFFICIAL
mariadb                         MariaDB Server is a high performing open sou…   5722      [OK]
mysql                           MySQL is a widely used, open-source relation…   15008     [OK]
phpmyadmin                      phpMyAdmin - A web interface for MySQL and M…   966       [OK]
percona                         Percona Server is a fork of the MySQL relati…   627       [OK]
circleci/mysql                  MySQL is a widely used, open-source relation…   29        

# 可选项
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results
      --no-trunc        Don't truncate output

# 示例
  --filter=STARS=3000	# 搜索出来的镜像就是STARS大于3000的
```

### docker pull

描述	从镜像仓库下载镜像
用法	`docker pull [OPTIONS] NAME[:TAG|@DIGEST]`

您的大多数镜像都将在基础镜像之上创建，这些镜像来自Docker Hub镜像仓库。

Docker Hub 中心包含许多预构建的镜像，您可以尝试，而无需定义和配置自己的。`pull`

要下载特定镜像或一组镜像（即存储库）， 使用。`docker pull`

#### 代理配置
如果您位于 HTTP 代理服务器后面，例如在公司设置中， 在打开连接到仓库之前，您可能需要配置 Docker 守护进程的代理设置，有关详细信息，请参阅 [dockerd 命令行参考](https://docs.docker.com/reference/cli/dockerd/#proxy-configuration)。

#### 并发下载
默认情况下，Docker 守护程序将一次拉取映像的三层。 如果您使用的是低带宽连接，这可能会导致超时问题，您可能需要降低 这是通过守护程序选项实现的。有关更多详细信息，请参阅[守护程序文档](https://docs.docker.com/reference/cli/dockerd/)。`--max-concurrent-downloads`

#### 选项


| 参数                    | 缺省 | 描述                                         |
| ----------------------- | ---- | -------------------------------------------- |
| -a, --all-tags          |      | 下载仓库中所有标记的镜像                     |
| --disable-content-trust | true | 跳过图像验证                                 |
| --platform              |      | `API 1.32+ `如果服务器支持多平台，则设置平台 |
| -q, --quiet             |      | 禁止详细输出                                 |

```
# 下载镜像的命令：docker pull 镜像名[:tag]
[root@192 ~]# docker pull mysql
Using default tag: latest		# 如果不写 tag，默认就是latest
latest: Pulling from library/mysql
2ba873cb070a: Pull complete 		# 分层下载，docker image的核心，联合文件系统
dd1a4da808dd: Pull complete 
3292fb4adf41: Pull complete 
3811c45068cc: Pull complete 
e13320244c05: Pull complete 
6a34d702f281: Pull complete 
de90f4481477: Pull complete 
d575200ae375: Pull complete 
aea400be5707: Pull complete 
38c930606a4f: Pull complete 
Digest: sha256:0f2e15fb8b47db2518b1428239ed3e3fe6a6693401b2cf19552063562cfc2fc4	#签名信息，也就是防伪标识
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest		# 真实地址

# 下面的两个命令是等价的
docker pull docker.io/library/mysql:latest 等价与 docker pull mysql

# 指定版本下载
[root@192 ~]# docker pull python:3.9-slim-bullseye
3.9-slim-bullseye: Pulling from library/python
04e7578caeaa: Pull complete 
97413375e23b: Pull complete 
8153a73f01c8: Pull complete 
579b68351ad8: Pull complete 
e30845563140: Pull complete 
Digest: sha256:4699b511fd5a0bf93f8067749285f040d593709dbb46016334556c972f055099
Status: Downloaded newer image for python:3.9-slim-bullseye
docker.io/library/python:3.9-slim-bullseye
```

### docker rmi

描述：删除一个或多个镜像
用法：	`docker rmi [OPTIONS] IMAGE [IMAGE...]`

从主机节点中删除（并取消标记）一个或多个镜像。如果镜像有多个标签，使用此命令并将标签作为参数仅删除标签。如果标签是镜像的唯一标签，则镜像和标签都被删除。

这不会从仓库中删除镜像。您无法删除正在运行容器的镜像，除非使用强制参数 `-f` 。
查看主机上的所有镜像使用 `docker images` 命令。

#### 选项
| 参数        | 描述                 |
| ----------- | -------------------- |
| -f, --force | 强制删除图像         |
| --no-prune  | 不要删除未标记的父项 |
```
[root@192 ~]#docker rmi -f 镜像id	# 删除指定的镜像
[root@192 ~]#docker rmi -f 镜像id 镜像id 镜像id……		# 删除多个镜像
[root@192 ~]# docker rmi -f $(docker images -aq)	# 删除全部的镜像
```

## 容器命令

说明：我们有了镜像才可以创建容器，在Linux中下载一个CentOS镜像来测试学习。
```
docker pull centos
```
### 新建容器并启动
`docker run [可选参数] 镜像`

```
docker run [可选参数] image

# 常用参数说明
--name="Name"	# 起一个容器名字，比如tomcat01、tomcat02……
-d		# 后台方式运行
-it		# 使用交互方式运行，进入容器查看内容
-p		# 指定容器的端口 -p 8080:8080
	-p ip:主机端口：容器端口
	-p 主机端口：容器端口（常用）
	-p 容器端口
	容器端口
-P		# 随机指定端口
```
测试，启动并进入容器
```
[root@192 ~]# docker run -it centos /bin/bash
[root@e663c4f0b596 /]# ls		# 查看容器内的CentOS，基础版本，很多命令都是不完善的。
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```
从容器中退回主机，并停止容器
```
[root@e663c4f0b596 /]# exit		# 直接停止并退出容器
exit
[root@192 ~]# ls
anaconda-ks.cfg  Clash for Windows-0.20.39-x64-linux  Desktop    Downloads  Pictures  Python-3.5.0      Templates  Videos
chatglm.cpp      Clash.for.Windows-0.20.zip           Documents  Music      Public    Python-3.5.0.tgz  tsz.txt
```
不停止容器，直接退出到主机 <kbd>Ctrl</kbd>+<kbd>p</kbd>+<kbd>q</kbd> 

### docker ps

描述：列出容器
用法：`docker ps [OPTIONS]`

#### 选项
| 参数         | 缺省 | 描述                                                                                                                                                                                                                                                                                                            |
| ------------ | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -a, --all    |      | 显示所有容器（默认显示正在运行）                                                                                                                                                                                                                                                                                |
| -f, --filter |      | 根据提供的条件筛选输出                                                                                                                                                                                                                                                                                          |
| --format     |      | 使用自定义模板设置输出格式：<br />“table”：使用列标题以表格格式打印输出（默认）<br />“table TEMPLATE”：使用给定的 Go 模板以表格格式打印输出<br />“json”：以 JSON 格式打印<br />“TEMPLATE”：使用给定的 Go 模板打印输出。<br />参考https://docs.docker.com/go/formatting/<br />有关使用模板设置输出格式的详细信息 |
| -n, --last   | -1   | 显示 n 个上次创建的容器（包括所有状态）                                                                                                                                                                                                                                                                         |
| -l, --latest |      | 显示最新创建的容器（包括所有状态）                                                                                                                                                                                                                                                                              |
| --no-trunc   |      | 不要截断输出                                                                                                                                                                                                                                                                                                    |
| -q, --quiet  |      | 仅显示容器 ID                                                                                                                                                                                                                                                                                                   |
| -s, --size   |      | 显示文件总大小                                                                                                                                                                                                                                                                                                  |

#### 用法实例
```
# docker ps 命令
-a		# 显示所有容器（默认显示正在运行）
-n=?		# 显示 n 个上次创建的容器（包括所有状态）
-q		# 仅显示容器 ID

[root@192 ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@192 ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS                     PORTS     NAMES
e663c4f0b596   centos         "/bin/bash"   9 minutes ago   Exited (0) 4 minutes ago             awesome_jones
365d43d7c584   d2c94e258dcb   "/hello"      8 days ago      Exited (0) 8 days ago                sweet_ptolemy


```

### docker rm

描述：删除一个或多个容器
用法：`docker rm [OPTIONS] CONTAINER [CONTAINER...]`

#### 选项
| 参数          | 描述                                   |
| ------------- | -------------------------------------- |
| -f, --force   | 强制移除正在运行的容器（使用 SIGKILL） |
| -l, --link    | 删除指定的链接                         |
| -v, --volumes | 删除与容器关联的匿名卷                 |

#### 用法实例
```
docker rm 容器id		# 删除指定的容器
docker rm -f $(docker ps -aq)	# 删除所有的容器
docker ps -a -q|xargs docker rm	# 删除所有的容器（感觉没有 -f 参考，不太严谨）
```

### docker start
`docker start 容器id`		# 启动容器
### dokcer stop
`docker stop 容器id`		# 停止当前正在运行的容器


描述：终止一个或多个正在运行的容器
用法：`docker kill [OPTIONS] CONTAINER [CONTAINER...]`

子命令会终止一个或多个容器。容器内的主进程会收到信号（默认信号），或者是使用选项指定的信号。您可以通过容器的ID、ID前缀或名称来引用容器。 `docker kill` `SIGKILL` `--signal`

该标志设置发送到容器的系统调用信号。例如，此信号可以是格式为 的信号名称，也可以是与内核系统调用表中的位置匹配的无符号数字，例如。`--signal` `SIG<NAME>` `SIGINT` `2`

虽然默认的（）信号会终止容器，但是通过设置的信号可能是非终止的，这取决于容器的主进程。例如，在大多数情况下，信号将是非终止的，容器在接收到信号后会继续运行。`SIGKILL` `--signal` `SIGHUP`

挖坑：**以上原官网个命令排版应该有问题，以后我学会了在重新排版**

#### 注意

`ENTRYPOINT`和以 shell 形式运行的子进程不会传递信号。这意味着可执行文件不是容器的 PID 1，也不会接收 Unix 信号。`CMD` `/bin/sh -c`

#### 选项
| 参数         | 描述             |
| ------------ | ---------------- |
| -s, --signal | 发送到容器的信号 |

#### 示例
发送一个KILL信号给一个容器：`SIGKILL` `my_container`
```
docker kill my_container
```
发送一个自定义信号给一个容器`（--signal）`
以下示例向名为：`my_container`的容器发送信号`SIGHUP` 
```
docker kill --signal=SIGHUP  my_container
```
您可以通过名称或编号指定自定义信号。前缀是可选的，因此以下示例是等效的：`SIG`
```
docker kill --signal=SIGHUP my_container
docker kill --signal=HUP my_container
docker kill --signal=1 my_container
```
请参考[signal(7)](https://man7.org/linux/man-pages/man7/signal.7.html)手册页，查看标准Linux信号列表。
### docker restart
`docker restart 容器id`		# 重启容器容器
### docker kill
`docker kill 容器id`		# 强制停止当前容器

