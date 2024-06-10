---
title: 通过 mac 地址查找 ip
description: "起因是我需要知道打印机的 IP，直接修改打印驱动端口 IP 地址。"
# linkTitle:
date: 2024-04-14T03:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 3
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
  - MAC
  - IP
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

# 通过mac地址查找IP

  　　————2024.4.20

## 起因
我在我自己办公室参加视频会，不方便离开办公室，但需要打印一点PDF文件。打印时发现办公室打印机连接不上，应该是 IP 地址又变了。

我需要知道打印机的 IP，直接修改打印驱动端口IP地址。

## 参考内容
* [思想流浪者【通过mac地址查找ip】](https://blog.csdn.net/qq_30346413/article/details/117412584)
* [yongbang_yan【centos7 nmap网络扫描工具的使用】](https://blog.csdn.net/weixin_41515615/article/details/84623616)

## 方法一：利用nmap扫描 192.168.110.0 网段
### nmap网络扫描工具简介

NMap，也就是Network Mapper，最早是Linux下的网络扫描和嗅探工具包。

其基本功能有三个:
1. 一是探测一组主机是否在线；
2. 其次是扫描 主机端口，嗅探所提供的网络服务；
3. 还可以推断主机所用的操作系统 。

Nmap可用于扫描仅有两个节点的LAN，直至500个节点以上的网络。Nmap 还允许用户定制扫描技巧。通常，一个简单的使用ICMP协议的ping操作可以满足一般需求；也可以深入探测UDP或者TCP端口，直至主机所 使用的操作系统；还可以将所有探测结果记录到各种格式的日志中， 供进一步分析操作。

### 安装nmap

运行`rpm -vhU https://nmap.org/dist/nmap-7.70-1.x86_64.rpm`

```
[root@localhost ~]# rpm -vhU https://nmap.org/dist/nmap-7.70-1.x86_64.rpm
Retrieving https://nmap.org/dist/nmap-7.70-1.x86_64.rpm
Preparing...                          ################################# [100%]
Updating / installing...
   1:nmap-2:7.70-1                    ################################# [100%]
```

 我上官网 https://nmap.org/ 查询最新的版本为 `nmap-7.94-1.x86_64.rpm` ，安装最新版时需要 Python 版本大于3.0，我暂时放弃安装最新版，按贴主的版本安装的。
 ```
[root@localhost ~]# rpm -vhU https://nmap.org/dist/nmap-7.94-1.x86_64.rpm
Retrieving https://nmap.org/dist/nmap-7.94-1.x86_64.rpm
error: Failed dependencies:
	python >= 3.0 is needed by nmap-2:7.94-1.x86_64
```

### nmap工具使用方法
进行ping扫描，打印出对扫描做出响应的主机,不做进一步测试(如端口扫描或者操作系统探测)：
nmap -sP 192.168.1.0/24

仅列出指定网络上的每台主机，不发送任何报文到目标主机：
nmap -sL 192.168.1.0/24

探测目标主机开放的端口，可以指定一个以逗号分隔的端口列表(如-PS22，23，25，80)：
nmap -PS 192.168.1.234

使用UDP ping探测主机：
nmap -PU 192.168.1.0/24

使用频率最高的扫描选项：SYN扫描,又称为半开放扫描，它不打开一个完全的TCP连接，执行得很快：
nmap -sS 192.168.1.0/24

当SYN扫描不能用时，TCP Connect()扫描就是默认的TCP扫描：
nmap -sT 192.168.1.0/24

UDP扫描用-sU选项,UDP扫描发送空的(没有数据)UDP报头到每个目标端口:
nmap -sU 192.168.1.0/24

确定目标机支持哪些IP协议 (TCP，ICMP，IGMP等):
nmap -sO 192.168.1.19

探测目标主机的操作系统：
nmap -O 192.168.1.19
nmap -A 192.168.1.19

另外，nmap官方文档中的例子：
nmap -v scanme.

这个选项扫描主机scanme中 所有的保留TCP端口。选项-v启用细节模式。
nmap -sS -O scanme./24

进行秘密SYN扫描，对象为主机Saznme所在的“C类”网段 的255台主机。同时尝试确定每台工作主机的操作系统类型。因为进行SYN扫描 和操作系统检测，这个扫描需要有根权限。
nmap -sV -p 22，53，110，143，4564 198.116.0-255.1-127

进行主机列举和TCP扫描，对象为B类188.116网段中255个8位子网。这 个测试用于确定系统是否运行了sshd、DNS、imapd或4564端口。如果这些端口 打开，将使用版本检测来确定哪种应用在运行。
nmap -v -iR 100000 -P0 -p 80

随机选择100000台主机扫描是否运行Web服务器(80端口)。由起始阶段 发送探测报文来确定主机是否工作非常浪费时间，而且只需探测主机的一个端口，因 此使用-P0禁止对主机列表。
nmap -P0 -p80 -oX logs/pb-port80scan.xml -oG logs/pb-port80scan.gnmap 216.163.128.20/20

扫描4096个IP地址，查找Web服务器(不ping)，将结果以Grep和XML格式保存。
host -l | cut -d -f 4 | nmap -v -iL -

进行DNS区域传输，以发现中的主机，然后将IP地址提供给 Nmap。上述命令用于GNU/Linux -- 其它系统进行区域传输时有不同的命令。
其他选项：
-p (只扫描指定的端口)
单个端口和用连字符表示的端口范 围(如 1-1023)都可以。当既扫描TCP端口又扫描UDP端口时，可以通过在端口号前加上T: 或者U:指定协议。 协议限定符一直有效直到指定另一个。 例如，参数 -p U:53，111，137，T:21-25，80，139，8080 将扫描UDP 端口53，111，和137，同时扫描列出的TCP端口。
-F (快速 (有限的端口) 扫描)

总结：实际环境使用的时候可以写个小脚本做个定时任务对系统进行扫描，将结果输出到指定文件。方便查看。具体自己研究！

### 方法一具体操作：扫描 192.168.110.0 网段

运行`nmap -sn 192.168.110.0/24`

```
[root@localhost ~]# nmap -sn 192.168.110.0/24
Starting Nmap 7.70 ( https://nmap.org ) at 2024-04-20 10:26 CST
Nmap scan report for localhost (192.168.110.1)
Host is up (0.0055s latency).
MAC Address: 64:6E:97:C0:EB:89 (Unknown)
Nmap scan report for localhost (192.168.110.2)
Host is up (0.0053s latency).
MAC Address: EC:C8:9C:4A:04:93 (Unknown)
……
Nmap scan report for localhost (192.168.110.40)
Host is up (0.014s latency).
MAC Address: 00:0E:C6:7A:49:A7 (Asix Electronics)
……
Nmap scan report for localhost (192.168.110.147)		# 搜索到了我们自己的打印机IP
Host is up (0.0027s latency).
MAC Address: 9C:93:4E:66:77:DD (Xerox)
……
Nmap scan report for localhost (192.168.110.150)		# 我自己的电脑主机IP
Host is up.
Nmap done: 256 IP addresses (159 hosts up) scanned in 15.80 seconds

```
## 方法二：查看主机上arp文件，根据 mac 地址查找ip

`/proc/net/arp`包含了一个可读的内核ARP表的ASCII转储，用于地址解析。
它将显示动态学习和预编程的ARP条目。

执行 `cat /proc/net/arp | grep mac地址`

 ```
 [root@localhost ~]# cat /proc/net/arp
IP address       HW type     Flags       HW address            Mask     Device
192.168.110.147  0x1         0x2         9c:93:4e:66:77:dd     *        ens33
192.168.110.1    0x1         0x2         64:6e:97:c0:eb:89     *        ens33
192.168.110.149  0x1         0x2         b4:69:21:c8:15:7c     *        ens33
192.168.110.27   0x1         0x2         e8:d8:d1:97:12:7d     *        ens33
192.168.110.250  0x1         0x2         f8:0d:ac:e9:7a:cd     *        ens33
……
[root@localhost ~]# 
```

## 另外：windows 扫描获取ip
### 批量ping局域网内ip

      `for /L %i IN (1,1,254) DO ping -w 2 -n 1 10.8.1.%i`

试验了一下，这个功能太傻，不好用。
```
C:\Users\Super Typhoon>for /L %i IN (1,1,254) DO ping -w 2 -n 1 10.8.1.%i

C:\Users\Super Typhoon>ping -w 2 -n 1 10.8.1.1

正在 Ping 10.8.1.1 具有 32 字节的数据:
请求超时。

10.8.1.1 的 Ping 统计信息:
    数据包: 已发送 = 1，已接收 = 0，丢失 = 1 (100% 丢失)，

C:\Users\Super Typhoon>ping -w 2 -n 1 10.8.1.2

正在 Ping 10.8.1.2 具有 32 字节的数据:
请求超时。

10.8.1.2 的 Ping 统计信息:
    数据包: 已发送 = 1，已接收 = 0，丢失 = 1 (100% 丢失)，

C:\Users\Super Typhoon>ping -w 2 -n 1 10.8.1.3

正在 Ping 10.8.1.3 具有 32 字节的数据:
请求超时。

10.8.1.3 的 Ping 统计信息:
    数据包: 已发送 = 1，已接收 = 0，丢失 = 1 (100% 丢失)，

C:\Users\Super Typhoon>ping -w 2 -n 1 10.8.1.4

正在 Ping 10.8.1.4 具有 32 字节的数据:
请求超时。

10.8.1.4 的 Ping 统计信息:
    数据包: 已发送 = 1，已接收 = 0，丢失 = 1 (100% 丢失)，

C:\Users\Super Typhoon>ping -w 2 -n 1 10.8.1.5

正在 Ping 10.8.1.5 具有 32 字节的数据:
请求超时。

10.8.1.5 的 Ping 统计信息:
    数据包: 已发送 = 1，已接收 = 0，丢失 = 1 (100% 丢失)，
```

### 显示地址解析协议(ARP)使用的“IP 到物理”地址转换表

运行  `arp -a | grep "mac地址"`

这个好用：
```
C:\Users\Super Typhoon>arp -a

接口: 192.168.56.1 --- 0xf
  Internet 地址         物理地址              类型
  192.168.56.255        ff-ff-ff-ff-ff-ff     静态
  224.0.0.2             01-00-5e-00-00-02     静态
  224.0.0.22            01-00-5e-00-00-16     静态
  224.0.0.251           01-00-5e-00-00-fb     静态
  224.0.0.252           01-00-5e-00-00-fc     静态
  239.255.255.250       01-00-5e-7f-ff-fa     静态
  255.255.255.255       ff-ff-ff-ff-ff-ff     静态

接口: 192.168.2.1 --- 0x12
  Internet 地址         物理地址              类型
  192.168.2.255         ff-ff-ff-ff-ff-ff     静态
  224.0.0.2             01-00-5e-00-00-02     静态
  224.0.0.22            01-00-5e-00-00-16     静态
  224.0.0.251           01-00-5e-00-00-fb     静态
  224.0.0.252           01-00-5e-00-00-fc     静态
  239.255.255.250       01-00-5e-7f-ff-fa     静态
  255.255.255.255       ff-ff-ff-ff-ff-ff     静态

接口: 192.168.110.149 --- 0x13
  Internet 地址         物理地址              类型
  192.168.110.1         64-6e-97-c0-eb-89     动态
  192.168.110.9         30-24-a9-61-41-8f     动态
  192.168.110.27        e8-d8-d1-97-12-7d     动态
  192.168.110.31        a4-5e-60-d7-ba-d5     动态
  ……
  192.168.110.147       9c-93-4e-66-77-dd     动态		# 办公室打印机地址
  192.168.110.150       00-0c-29-09-3d-c1     动态
  ……
  192.168.110.247       1c-7d-22-44-86-f8     动态
  192.168.110.250       f8-0d-ac-e9-7a-cd     动态
  192.168.110.255       ff-ff-ff-ff-ff-ff     静态
  224.0.0.2             01-00-5e-00-00-02     静态
  224.0.0.22            01-00-5e-00-00-16     静态
  224.0.0.113           01-00-5e-00-00-71     静态
  224.0.0.251           01-00-5e-00-00-fb     静态
  224.0.0.252           01-00-5e-00-00-fc     静态
  239.255.255.250       01-00-5e-7f-ff-fa     静态
  239.255.255.253       01-00-5e-7f-ff-fd     静态
  255.255.255.255       ff-ff-ff-ff-ff-ff     静态

接口: 169.254.66.40 --- 0x15
  Internet 地址         物理地址              类型
  169.254.255.255       ff-ff-ff-ff-ff-ff     静态
  224.0.0.2             01-00-5e-00-00-02     静态
  224.0.0.22            01-00-5e-00-00-16     静态
  224.0.0.251           01-00-5e-00-00-fb     静态
  224.0.0.252           01-00-5e-00-00-fc     静态
  239.255.255.250       01-00-5e-7f-ff-fa     静态
  255.255.255.255       ff-ff-ff-ff-ff-ff     静态

C:\Users\Super Typhoon>
```