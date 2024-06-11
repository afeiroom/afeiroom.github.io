---
title: 常用命令小结
description: "常用命令小结。"
# linkTitle:
date: 2024-04-19T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 5
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

# 常用命令小结


![Docker-commands-Summary.png](https://s2.loli.net/2024/06/11/6ism2zINfv4ydjA.png)


```
attach		# 当前shell下attach 连接指定运行镜像
build		# 通过Dockerfile 定制镜像
commit		# 提交当前容器为新的镜像
cp		# 从容器中拷贝指定文件或者目录到宿主机中
create		# 创建一个新的容器，同run. 但不启动容器
diff		# 查看docker 容器变化
events		# 从docker 服务获取容器实时事件
exec		# 在已存在的容器上运行命令
export		# 导出容器的内容流作为一个tar 归档文件[对应import ]
history		# 展示一个镜像形成历史
images		# 列出系统当前镜像
import		# 从tar包中的内容创建一个新的文件系统映像[对应export]
info		# 显示系统相关信息
inspect		# 查看容器详细信息
ki11 		# ki1l指定docker容器
load		# 从一个tar包中加载一个镜像[对应save]
login		# 注册或者登陆一个docker 源服务器
logout		# 从当前Docker registry退出
1ogs		# 输出当前容器日志信息
port		# 查看映射端口对应的容器内部源端口
pause		# 暂停容器
ps		# 列出容器列表
pu11		# 从docker镜像源服务器拉取指定镜像或者库镜像
push		# 推送指定镜像或者库镜像至docker源服务器
restart		# 重启运行的容器
rm		# 移除一个或者多个容器
rmi		# 移除一个或多个镜像[无容器使用该镜像才可删除，否则需删除相关容器才可继续或-f强制删除]
run		# 创建一个新的容器并运行一个命令
save		# 保存一个镜像为一个tar包[对应load]
search		# 在docker hub 中搜索镜像
start		# 启动容器
stop		# 停止容器
top		# 查看容器中运行的进程信息
unpause		# 取消暂停容器
version		# 查看docker 版本号
wait		# 截取容器停止时的退出状态值
```

docker 的命令是非常多的，上面我们学习的那些都是最常用的容器和镜像命令，之后我们还会学习很多命令！

> 接下来就是一堆的练习

