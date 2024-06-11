---
title: 日志、元数据、进程的查看
description: "Docker的常用命令。"
# linkTitle:
date: 2024-04-17T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 3
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

# 日志、元数据、进程的查看

## 后台启动容器
```
# 命令 docker run -d 镜像名！
[root@localhost ~]# docker run -d centos
cc5d8ec7244323c10fbfadbf44846c5d45ad50e60ac6df9f171407933956f725

# 问题：docker ps，发现 centos 运行过，但又停止了
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@localhost ~]# docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS                      PORTS     NAMES
cc5d8ec72443   centos         "/bin/bash"   53 seconds ago   Exited (0) 51 seconds ago             nostalgic_faraday
e663c4f0b596   centos         "/bin/bash"   41 hours ago     Exited (0) 41 hours ago               awesome_jones
365d43d7c584   d2c94e258dcb   "/hello"      10 days ago      Exited (0) 10 days ago                sweet_ptolemy
[root@localhost ~]# 

# 常见的坑，docker 容器使用后台运行，就必须要有一个前台进程，docker发现没有应用，就会自动停止。
# nginx，容器启动后，发现自己没有提供服务，就会利己停止，就是没有程序了。
```

## 查看日志
```
docker logs
```

Docker 容器日志
描述：获取容器的日志
用法：`docker logs [OPTIONS] CONTAINER`

该命令批量检索执行时存在的日志。`docker logs`

有关选择和配置日志记录驱动程序的详细信息，请参阅[配置日志记录驱动程序](https://docs.docker.com/config/containers/logging/configure/)。

该命令`docker logs --follow` 将继续从容器的`STDOUT`和`STDERR`中流式传输新的输出。

将负数或非整数传递给`--tail`是无效的，在这种情况下，该值设置为`all`。

该命令`docker logs --timestamps`将添加一个 [RFC3339Nano](https://pkg.go.dev/time#RFC3339Nano) 时间戳，例如`2014-09-16T06:17:46.000000000Z`，到每个 日志条目。为确保时间戳对齐，必要时，时间戳的纳秒部分将填充为零。

该命令`docker logs --details`将添加额外的属性，例如 环境变量和标签，在创建 容器。 `--log-opt`

该选项仅显示给定日期之后生成的容器日志。 您可以将日期指定为 RFC 3339 日期、UNIX 时间戳或 Go 持续时间字符串（例如 , ）。 除了 RFC3339 日期格式之外，您还可以使用 RFC3339Nano、 、 、 和 。 如果您未在时间戳末尾提供 或时区偏移量，则将使用客户端上的本地时区。 提供 Unix 时间戳时，输入秒[.nanoseconds]，其中秒是自 1970 年 1 月 1 日（UTC/GMT 午夜）以来经过的秒数，不包括闰秒（又名 Unix 纪元或 Unix 时间），以及可选的 . 纳秒字段是秒的一小部分，长度不超过九位数字。 您可以将该选项与 或 选项中的一个或两个结合使用。`--since` `1m30s` `3h` `2006-01-02T15:04:05` `2006-01-02T15:04:05.999999999` `2006-01-02Z07:00` `2006-01-02` `Z` `+-00:00` `--since` `--follow` `--tail`

### 选项
| 参数             | 缺省 | 描述                                                                               |
| ---------------- | ---- | ---------------------------------------------------------------------------------- |
| --details        |      | 显示提供给日志的额外详细信息                                                       |
| -f, --follow     |      | 关注日志输出                                                                       |
| --since          |      | 显示自时间戳（例如`2013-01-02T13:23:37Z`）<br />或相对（例如 42分钟` 42m`）        |
| -n, --tail       | all  | 从日志末尾显示的行数                                                               |
| -t, --timestamps |      | 显示时间戳                                                                         |
| --until          |      | `API 1.35+`在时间戳（例如`2013-01-02T13:23:37Z`）<br />或相对（例如 42分钟` 42m`） |

### 示例
查看日志
```
docker logs -f -t --tail 容器id   # 运行发现没有日志，因为容器停止运行，没有日志输出。

# 自己写一段shell脚本
[root@localhost ~]# docker run -d centos /bin/sh -c "while true;do echo Afei;sleep 1;done"

# 查看正在运行的容器
[root@localhost ~]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS     NAMES
9c6120f0c6b0   centos    "/bin/sh -c 'while t…"   About a minute ago   Up About a minute             pedantic_ramanujan

# 显示日志，常用参数
  -f, --follow         # 关注日志，持续输出
  -n, --tail string    # 从日志末尾显示的行数 (默认为 "all")
  -t, --timestamps     # 显示时间戳

[root@localhost ~]# docker logs -tf --tail 10 9c6120f0c6b0
2024-04-18T09:56:49.243959580Z Afei
2024-04-18T09:56:50.246589121Z Afei
2024-04-18T09:56:51.249313684Z Afei
2024-04-18T09:56:52.252134488Z Afei
2024-04-18T09:56:53.254821997Z Afei
2024-04-18T09:56:54.261482802Z Afei
2024-04-18T09:56:55.269578175Z Afei
2024-04-18T09:56:56.273772986Z Afei
2024-04-18T09:56:57.276367170Z Afei
2024-04-18T09:56:58.279728057Z Afei
2024-04-18T09:56:59.283156036Z Afei
2024-04-18T09:57:00.285945557Z Afei
……
```
## 查看容器中的进程信息
描述：显示容器的运行进程
用法：`docker top CONTAINER [ps OPTIONS]`

显示容器的运行进程

```
[root@localhost ~]# docker top 9c6120f0c6b0
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                6090                6068                0                   17:51               ?                   00:00:01            /bin/sh -c while true;do echo Afei;sleep 1;done
root                8614                6090                0                   18:24               ?                   00:00:00            /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1
[root@localhost ~]# 
```

## 查看镜像的元数据

描述：显示一个或多个容器的详细信息
用法：`docker inspect [OPTIONS] CONTAINER [CONTAINER...]`

显示一个或多个容器的详细信息

### 选项
| 参数         | 描述                                                                                                                                                                                               |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -f, --format | 使用自定义模板设置输出格式：<br />'json'：以 JSON 格式打印<br />'TEMPLATE'：使用给定的 Go 模板打印输出。<br />请参阅https://docs.docker.com/go/formatting/<br />有关使用模板设置输出格式的详细信息 |
| -s, --size   | 显示文件总大小                                                                                                                                                                                     |

### 示例
```
[root@localhost ~]# docker inspect 9c6120f0c6b0
[
    {
        "Id": "9c6120f0c6b0711cc655396b9c1ced4ad1d497b9988d931c4364b2ae98fd1b6c",	# 容器的ID
        "Created": "2024-04-18T09:51:36.952265573Z",	# 容器的创建时间
        "Path": "/bin/sh",				# 容器的控制台
        "Args": [
            "-c",
            "while true;do echo Afei;sleep 1;done"
        ],
        "State": {					# 容器的状态内容
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 6090,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-04-18T09:51:37.384573457Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:5d0da3dc976460b72c77d94c8a1ad043720b0416bfc16c52c45d4847e53fadb6",	# 创建容器的镜像信息
        "ResolvConfPath": "/var/lib/docker/containers/9c6120f0c6b0711cc655396b9c1ced4ad1d497b9988d931c4364b2ae98fd1b6c/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/9c6120f0c6b0711cc655396b9c1ced4ad1d497b9988d931c4364b2ae98fd1b6c/hostname",
        "HostsPath": "/var/lib/docker/containers/9c6120f0c6b0711cc655396b9c1ced4ad1d497b9988d931c4364b2ae98fd1b6c/hosts",
        "LogPath": "/var/lib/docker/containers/9c6120f0c6b0711cc655396b9c1ced4ad1d497b9988d931c4364b2ae98fd1b6c/9c6120f0c6b0711cc655396b9c1ced4ad1d497b9988d931c4364b2ae98fd1b6c-json.log",
        "Name": "/pedantic_ramanujan",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {					#主机的配置
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                25,
                87
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b648168473e17d494672a6d732b081caa5ab9de52e2cc225505f461389472fdd-init/diff:/var/lib/docker/overlay2/7a97237ae78c4b8fd2268117698dbffc01d5eb6383f33ecfeb32bcadba8f79cd/diff",
                "MergedDir": "/var/lib/docker/overlay2/b648168473e17d494672a6d732b081caa5ab9de52e2cc225505f461389472fdd/merged",
                "UpperDir": "/var/lib/docker/overlay2/b648168473e17d494672a6d732b081caa5ab9de52e2cc225505f461389472fdd/diff",
                "WorkDir": "/var/lib/docker/overlay2/b648168473e17d494672a6d732b081caa5ab9de52e2cc225505f461389472fdd/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],					# 挂载信息，目前没有挂载
        "Config": {					# 基本配置
            "Hostname": "9c6120f0c6b0",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [					# 基本的环境变量
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true;do echo Afei;sleep 1;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20210915",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {				# 网络的信息
            "Bridge": "",
            "SandboxID": "c701037a4d7b0069751caea79200f46d4078f89c2a5d45b903b4da85a7340370",
            "SandboxKey": "/var/run/docker/netns/c701037a4d7b",
            "Ports": {},
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "c14f24d1103bc61d67750ede4e8de15a45f6c318e24cc4f8e04a82a0e481c08c",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:11:00:02",
                    "NetworkID": "0f99e0ae85f95be5b9804956572bc7526d67876c39386eea9dee0c4d44184731",
                    "EndpointID": "c14f24d1103bc61d67750ede4e8de15a45f6c318e24cc4f8e04a82a0e481c08c",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DriverOpts": null,
                    "DNSNames": null
                }
            }
        }
    }
]
[root@localhost ~]# 
```