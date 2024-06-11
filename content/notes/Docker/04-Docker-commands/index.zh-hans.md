---
title: 进入容器的命令和拷贝命令
description: "进入容器的命令和拷贝命令。"
# linkTitle:
date: 2024-04-18T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 4
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

# 进入容器的命令和拷贝命令

  　　————2024.4.18
	
## docker exec 在正在运行的容器

描述：在正在运行的容器中执行命令
用法：`docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`
```
Docker Debug 简介

要轻松地将调试 shell 放入任何容器中，请使用 `docker debug`。Docker Debug 是使用 `docker exec`. 有了它，您可以将 shell 放入任何容器或镜像中，甚至是纤薄的容器或镜像，而无需进行修改。 另外，您可以在其可定制的工具箱中携带您最喜欢的调试工具。 

立即探索 [Docker Debug](https://docs.docker.com/reference/cli/docker/debug/)。
```

该命令在正在运行的容器中运行新命令。`docker exec`

您指定的命令仅在容器的主进程（）运行时运行，并且如果容器重新启动，则不会重新启动。docker exec PID 1

该命令在容器的默认工作目录中运行。

该命令必须是可执行文件。 链接或引用的命令不起作用。

这有效：`docker exec -it my_container sh -c "echo a && echo b"`
这不起作用：`docker exec -it my_container "echo a && echo b"`
### 选项
| 参数              | 描述                                             |
| ----------------- | ------------------------------------------------ |
| -d, --detach      | 分离模式：在后台运行命令                         |
| --detach-keys     | 覆盖用于分离容器的键序列                         |
| -e, --env         | `API 1.25+`设置环境变量                          |
| --env-file        | `API 1.25+`读取环境变量文件                      |
| -i, --interactive | 即使未连接，也要保持 STDIN 打开                  |
| --privileged      | 为命令授予扩展权限                               |
| -t, --tty         | 分配伪 TTY                                       |
| -u, --user        | 用户名或UID（格式：`<name\|uid>[:<group\|gid>])` |
| -w, --workdir     | `API 1.35+`容器内的工作目录                      |

### 示例

```
[root@192 ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS          PORTS     NAMES
f6272c9291e7   centos    "/bin/bash"               12 minutes ago   Up 12 minutes             mystifying_ardinghelli
9c6120f0c6b0   centos    "/bin/sh -c 'while t…"   3 hours ago      Up 4 minutes              pedantic_ramanujan
[root@192 ~]# docker exec -it f6272c9291e7 /bin/bash
[root@f6272c9291e7 /]# ps -ef
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 12:34 pts/0    00:00:00 /bin/bash
root         15      0  0 12:47 pts/1    00:00:00 /bin/bash
root         31     15  0 12:50 pts/1    00:00:00 ps -ef
```

## docker attach

描述：将本地标准输入、输出和错误流附加到正在运行的容器
用法：`docker attach [OPTIONS] CONTAINER`

用于使用容器的 ID 或名称将终端的标准输入、输出和错误（或三者的任意组合）附加到正在运行的容器。 这使您可以查看其输出或以交互方式控制它，就像命令直接在终端中运行一样。`docker attach`

> 注意
该命令显示容器和进程的输出。 这看起来好像附加命令被挂起，而实际上进程当时可能根本没有写入任何输出。`attach` `ENTRYPOINT` `CMD`

您可以同时多次附加到同一包含的进程， 来自 Docker 主机上的不同会话。

若要停止容器，请使用 .此密钥序列发送到 容器。如果为 true（默认值），则将 容器。如果容器与 和 一起运行，则可以从 一个容器，并使用键序列让它保持运行状态。`CTRL-c` `SIGKILL` `--sig-proxy` `CTRL-c` `SIGINT` `-i` `-t` `CTRL-p` `CTRL-q`

> 注意
在容器内作为 PID 1 运行的进程由 Linux：它通过默认操作忽略任何信号。所以，这个过程 不会终止，除非它被编码为这样做。SIGINTSIGTERM

您无法重定向命令的标准输入，而 附加到启用了 TTY 的容器（使用 和 选项）。`docker attach` `-i` `-t`

当客户端使用 ， 连接到容器时， Docker 使用 ~1MB 的内存缓冲区来最大化应用程序的吞吐量。 一旦此缓冲区已满，API 连接的速度就会受到影响，因此 这会影响输出进程的写入速度。这与其他类似 SSH 等应用程序。因此，不建议运行 性能关键型应用程序，在 客户端连接速度较慢的前景。请改用该命令来访问日志。`stdio` `docker attach` `docker logs`

### 选项
| 参数          | 缺省 | 描述                           |
| ------------- | ---- | ------------------------------ |
| --detach-keys |      | 覆盖用于分离容器的键序列       |
| --no-stdin    |      | 不附加 STDIN                   |
| --sig-proxy   | true | 将所有接收到的信号代理到进程中 |

### 示例
```
[root@192 ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS          PORTS     NAMES
f6272c9291e7   centos    "/bin/bash"               39 minutes ago   Up 39 minutes             mystifying_ardinghelli
9c6120f0c6b0   centos    "/bin/sh -c 'while t…"   3 hours ago      Up 32 minutes             pedantic_ramanujan
[root@192 ~]# docker attach 9c6120f0c6b0
Afei
Afei
Afei
Afei
……		# 进入到死循环里，出不来了，哈哈
```

### docker attach 与 docker exec 区别

#### exec和attach命令的简单区别

区别：是否开启一个新的线程
* docker exec 进入容器后开启一个新的终端，可以在里面操作(常用)
* docker attach 进入容器正在执行的终端，不会启动新的进程

#### 并发性
`docker exec` 可以在同一个容器中并行执行多个命令，而 `docker attach` 则只能连接到容器的一个单独进程。

#### 安全性
由于 `docker attach` 可能会导致容器主进程的意外终止，所以使用 `docker exec` 更安全。

#### 交互性
尽管 `docker attach` 可以用于交互，但如果需要在容器内部启动新的交互式会话，使用 `docker exec` 会更方便。


## docker cp 复制文件或文件夹

描述：在容器和本地文件系统之间复制文件/文件夹
用法：`docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|- docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH`

该实用程序`docker cp`将 `SRC_PATH` 的内容复制到 `DEST_PATH`。 您可以从容器的文件系统复制到本地计算机，或者相反，从本地文件系统复制到容器。`-` 如果为 `SRC_PATH` 或 `DEST_PATH` 指定，您还可以从 `STDIN` 或 `STDOUT` 向 `CONTAINER` 传输 tar 存档。 可以是正在运行或已停止的容器。  `SRC_PATH` 或 `DEST_PATH` 可以是文件或目录。        

该命令假定容器路径相对于容器的（根）目录。这意味着提供初始正斜杠是可选的; 该命令将 和 视为相同。本地计算机路径可以 是绝对值或相对值。该命令将本地机器的相对路径解释为相对于当前工作目录运行的路径。`docker cp` `/` `compassionate_darwin:/tmp/foo/myfile.txt` `compassionate_darwin:tmp/foo/myfile.txt` `docker cp`

该命令的行为类似于 Unix 命令，因为目录是 以递归方式复制，并尽可能保留权限。所有权设置为 目标中的用户和主组。例如，复制到 容器是使用 root 用户创建的。复制到本地的文件 机器是使用调用命令的用户创建的。但是，如果指定该选项，请设置所有权 到源中的用户和主组。 如果指定该选项，则遵循任何符号链接 在。 如果父目录不存在，则不会创建父目录。`cp` `cp -a` `UID:GID` `UID:GID` `docker cp` `-a` `docker cp` `-L` `docker cp` `SRC_PATH` `docker cp` `DEST_PATH`

假设路径分隔符为 `/`，第一个参数为 `SRC_PATH` 和 `DEST_PATH` 的参数，行为如下：  
*  `SRC_PATH` 指定文件
	* `DEST_PATH` 不存在
		* 该文件将保存到在以下位置创建的文件中 `DEST_PATH`
	* `DEST_PATH` 不存在，以 `/` 结尾
		* 错误条件：目标目录必须存在。
	* `DEST_PATH` 存在并且是一个文件
		* 目标被源文件的内容覆盖
	* `DEST_PATH` 存在并且是一个目录
		* 使用 `SRC_PATH` 中的 basename 将文件复制到此目录中
* `SRC_PATH` 指定目录
	* `DEST_PATH` 不存在
		* `DEST_PATH` 创建为目录和源的内容 目录被复制到此目录中
	* `DEST_PATH` 存在并且是一个文件
		* 错误条件：无法将目录复制到文件
	* `DEST_PATH` 存在并且是一个目录
		* `SRC_PATH` 不以（即：斜杠后跟点 `/.`） 结尾
			* 源目录将复制到此目录中
		* `SRC_PATH` 确实以（即：斜杠后跟点 `/.`） 结尾
			* 源目录的内容将复制到此目录中

该命令要求并根据上述内容存在 规则。如果是本地链接并且是符号链接，则符号链接，而不是 默认情况下，将复制目标。若要复制链接目标而不是链接，请指定 选项。`SRC_PATH` `DEST_PATH` `SRC_PATH` `-L`

冒号 （） 用作 和 之间的分隔符。您可以 在指定本地 OR 的路径时也使用 机器，例如.如果在本地计算机路径中使用 必须显式使用相对路径或绝对路径，例如：`:` `CONTAINER` `:` `SRC_PATH` `DEST_PATH` `file:name.txt` `:`

`/path/to/file:name.txt` or `./file:name.txt`

### 选项
| 参数              | 描述                                                           |
| ----------------- | -------------------------------------------------------------- |
| -a, --archive     | 存档模式（复制所有 uid/gid 信息）                              |
| -L, --follow-link | 始终遵循SRC_PATH中的符号链接                                   |
| -q, --quiet       | 在复制过程中禁止进度输出。如果未连接终端，则会自动抑制进度输出 |

### 示例

从容器内拷贝文件到主机上

`docker cp 容器id:容器内路径 目的地主机路径`
```
# 查看当前主机下的容器
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                   CREATED          STATUS                        PORTS     NAMES
3f5375db052f   centos         "/bin/bash"               11 minutes ago   Exited (0) 8 minutes ago                compassionate_brahmagupta
f6272c9291e7   centos         "/bin/bash"               20 hours ago     Exited (0) 9 hours ago                  mystifying_ardinghelli
[root@localhost ~]# docker start 3f5375db052f		# 启动一个停止的容器
3f5375db052f
[root@localhost ~]# docker ps		# 查看正在运行的容器
CONTAINER ID   IMAGE     COMMAND                   CREATED          STATUS          PORTS     NAMES
3f5375db052f   centos    "/bin/bash"               12 minutes ago   Up 14 seconds             compassionate_brahmagupta
9c6120f0c6b0   centos    "/bin/sh -c 'while t…"   23 hours ago     Up 27 minutes             pedantic_ramanujan
[root@localhost ~]# docker attach 3f5375db052f		# 进入docker容器内部
[root@3f5375db052f /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@3f5375db052f /]# cd home
[root@3f5375db052f home]# ls
test.java
[root@3f5375db052f home]# touch testcp.java		# 在容器内新建一个待拷贝的文件
[root@3f5375db052f home]# exit	# 退出该容器，尽管容器停止运行，但容器内部的文件依然存在，可以进行拷贝
exit
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED        STATUS          PORTS     NAMES
9c6120f0c6b0   centos    "/bin/sh -c 'while t…"   23 hours ago   Up 28 minutes             pedantic_ramanujan
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                   CREATED          STATUS                        PORTS     NAMES
3f5375db052f   centos         "/bin/bash"               14 minutes ago   Exited (0) 11 seconds ago               compassionate_brahmagupta
f6272c9291e7   centos         "/bin/bash"               20 hours ago     Exited (0) 9 hours ago                  mystifying_ardinghelli
[root@localhost ~]# docker cp 3f5375db052f:/home/testcp.java /root	# 将容器内的文件拷贝到主机的/root里
Successfully copied 1.54kB to /root
[root@localhost ~]# ls
Python-3.5.0.tgz  testcp.java  tsz.txt
```

拷贝是一个手动的过程，未来我们使用 -v 卷的技术，可以实现自动同步 容器内部的 `/home` 目录与主机的 `/home` 目录打通。