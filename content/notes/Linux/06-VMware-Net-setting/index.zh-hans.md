---
title: VMware 虚拟机配置 CentOS 7 网络
description: "CentOS 7 网络设置。"
# linkTitle:
date: 2024-04-25T03:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 6
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
  - VMware
  - 虚拟机
  - 配置网络
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

# VMware虚拟机配置 CentOS 7 网络

	
## 参考资料


[佛祖下的灯芯【CentOS 7教程（二）-网络设置】](https://zhuanlan.zhihu.com/p/79361590)

## 前言

Linux系统主要应用于服务器端，而服务器的管理，并不像我们操作PC一样，可以直接操作。

服务器一般是放在数据中心机房，而进入数据中心机房是需要严格的审核的，比如金属检测、身份认证、登记等手续。

服务器在安装完成后，很少进行现场操作了。

所以，对于Linux服务器，我们一般是采用SSH的远程操作。

而对于我们学习CentOS来说，最好也是保持这个习惯，毕竟学习这个是要用在服务器上的。

而使用SSH远程操作，则需要我们配置网络及使用特定的支持SSH的软件了。

## 一、网络设置

### （一）、虚拟机的网络

我们是使用虚拟机来进行安装CentOS 7，所以网络设置要先在VMware中进行，在真实的服务器中请无视这一环节。

关闭刚才安装的CentOS虚拟机电源，关闭VMware，然后在桌面的VMware图标中，鼠标右键，以管理员身份运行。假如这一步不做，在VMware中设置网络就会因为权限不足而导致失败。

打开编辑菜单，选择虚拟网络编辑器。进入到虚拟网络编辑器界面。

![Virtual-Network-Editor.webp](https://s2.loli.net/2024/06/10/P6YpmiyX3U419xv.webp)


在这个界面里， 有VMnet0、VMnet1、VMnet8三个网络名称，其分别对应了桥接模式、仅主机模式、NAT模式。

我们在安装的时候，网络的选项是使用NAT模式，对应则是VMnet8。

当然，如果我们忘记了选择了什么模式，可以在“编辑虚拟机设置”中再次打开查看，当然咯，需要更改配置的，需要先关闭虚拟机。

![virtual-machine-settings.webp](https://s2.loli.net/2024/06/10/Li3w941u2xrjVIU.webp)


选择VMnet8，取消“使用本地DHCP服务将IP地址分配给虚拟机”。我们自己来手工设置IP地址。

![Virtual-Network-Editor2.jpg](https://s2.loli.net/2024/06/10/alJRxQY2jzPwLZ8.jpg)


点开"NAT设置"，可以看到其网关是：192.168.149.2
```
我自己电脑的网关是：192.168.2.2
```
打开Windows的网络设置，在适配器中，看到了吧，有一个也叫VMnet8的网络适配器，VMware里的虚拟机就是通过这个虚拟的网络适配器与主机共享IP地址，从而实现网络通信的。

我们把Windows的VMnet8网络适配器手动设置一个IP地址。

设置什么IP地址呢？就设置VMware的虚拟网络编辑器里的DHCP的IP地址段吧。

IP：192.168.149.3
MASK：255.255.255.0
GATEWAY：192.168.149.2
```
我自己电脑的设置是：
	IP：192.168.2.1
	MASK：255.255.255.0
	GATEWAY： .  .  .

```

![Network-connection.jpg](https://s2.loli.net/2024/06/10/jKlEfdwOap72zqT.jpg)

好的，现在为止，虚拟机的虚拟网络IP设置好了。我们还需要设置CentOS操作系统的IP地址。

### （二）、CentOS设置网络

打开CentOS虚拟机，进入到桌面，我们按住Ctrl+Alt+F2三个键，进入到终端。此刻终端应该是让你输入登陆用户名和密码，我们就用安装时的root管理员账号和密码登陆。

当然，输入密码时，不会显示\***的，是什么都没有显示，照常输入就可以了，别管它，毕竟Linux和Windows还有有很大差别的。

当输入root账号和密码登陆后，光标如下图所示

![Centos-login.webp](https://s2.loli.net/2024/06/10/NUkprbTeaVZdMS2.webp)


我们来看看是什么意思。

root：代表了你是使用root账户登陆。

localhost：表示本机的机器名。

~：表示目前在家目录下。

#：是root根目录操作的特定符号，如果是其它账号登陆，则是$。

我们则是在#后面进行命令行的操作。

还记得教程（一）中提到的，Linux一切皆文件吗？对的，在Linux下，网络配置也是一个文件。

我们使用以下命令进行网络配置：vi /etc/sysconfig/network-scripts/ifcfg-ens33

![Centos-vi.jpg](https://s2.loli.net/2024/06/10/gfOcuRPbC5UIStd.jpg)


解析一下这个命令。

vi：是Linux下的一个文本编辑器。以上的命令是指用vi打开/etc/sysconfig/network-scripts/ifcfg-ens33这个文件，ifcfg-ens33就是CentOS下的网络配置文件。

那么，我记不全地址怎么办？当然，也可以按Tab键进行自动补全，比如，当输入vi /etc/sysc时，再按Tab键，就会自动补全目录名称了。

进入到ifcfg-ens33这个文件，如下图。

![Centos-ifcfg-ens33.webp](https://s2.loli.net/2024/06/10/Qo6Ye1cnPw5dTX7.webp)


```
##我的电脑显示如下（已经完成设置的情况）：
[root@192 ~]# vi /etc/sysconfig/network-scripts/ifcfg-ens33

TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp		# dhcp 是“动态主机配置协议”，表示自动获取 IP 地址；static 是静态 IP 地址。
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=6f1ca908-c4b4-4ce3-9ae4-0fa8f106a99a
DEVICE=ens33
ONBOOT=yes		#  onboot=yes 或者 no 的意思是是否激活网卡，激活后就可以连接到外网了。

### 由于本人是笔记本电脑，经常移动办公，所以没有设置为“静态 IP ”。
```
整个屏幕被分成两部分，上面的内容，下面是命令行（目前在显示文件的路径）。

如果用Windows的文件编辑器的理解，你会发现，目前无法你键盘输入什么，都不会有反应。

我们尝试按一下I或者A键。下午命令行变成了-- INSERT--，对的，这就是输入模式。

![Centos-ifcfg-ens33-2.webp](https://s2.loli.net/2024/06/10/WFyr9Gvf1UIN5J3.webp)


我们利用上下箭头键，移动光标到最后，输入或修改以下内容：

IPADDR=192.168.149.88

NETMASK=255.255.255.0

GATEWAY=192.168.149.2

ONBOOT=yes

BOOTPROTO=static

完成后，我们按下ESC键，然后是:wq！，注意，是先按下冒号，再输入wq！

按下冒号，代表进入到命令行模式，wq!表是强制保存文件并退出。


![Centos-ifcfg-ens33-3.webp](https://s2.loli.net/2024/06/10/flas4OdCY5xnbvt.webp)

### （三）、重新启动系统
好了，网络的配置文件就修改好了，执行以下命令进行重启Linux：

reboot

重启CentOS后，我们使用Windows来Ping一下192.168.149.88这个IP，发现可以正常通信了。


![Ping.webp](https://s2.loli.net/2024/06/10/keVgiClWLt1JGRS.webp)


好了，现在虚拟机和物理机之间就可以通过VMnet8这个虚拟网络正常通信了。

如果发现还是无法Ping通，可以尝试禁用VMnet8这个网络，再启用，这样可以消除之前网络DHCP的影响。

## 二、小结

虚拟机是通过虚拟网络与现实网络通信的，虚拟网络在Windows的网络设置里就有。

vi /etc/sysconfig/network-scripts/ifcfg-ens33这个命令是编辑CentOS里的网络设置，vi是编辑命令，ifcfg-ens33是网卡的文件。

在vi界面里，按下i或者a键可以进入到编辑模式，按下ESC键进入到命令行模式，:wq!是强制保存并退出，w代表write的意思，q代表quit的意思。

码字不易，谢谢大家点赞。
