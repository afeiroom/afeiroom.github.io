---
title: 在 Linux 上安装 Hugo
description: "Hugo官网 Install Hugo on Linux 安装说明文档。"
# linkTitle:
date: 2024-04-27T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 3
nav_icon:
  vendor: bootstrap
  name: columns-gap
  color: BlueViolet
series:
  - Hugo
categories:
  - 笔记
tags:
  - Hugo
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

# 在 Linux 上安装 Hugo

	
## 参考内容

* 安装说明翻译[Hugo官网【在 Linux 上安装 Hugo】](https://gohugo.io/installation/linux/)
* 操作步骤参考[兮动人的博客【Centos7.3、nginx环境下部署hugo博客】](https://cloud.tencent.com/developer/article/1834210)

## 安装说明

以下是 Hugo官网 Install Hugo on Linux.安装说明文档：

* 版本
Hugo 有两个版本：标准版和扩展版。使用扩展版，您可以：
	* 处理图像时编码为 WebP 格式。您可以使用任一版本解码 WebP 图像。
	* 使用嵌入式 LibSass 转译器将 Sass 转译为 CSS。使用 Dart Sass 转译器不需要扩展版本。

* 我们建议您安装扩展版。

* 先决条件
虽然并非在所有情况下都需要，但在使用 Hugo 时通常使用 [Git](https://git-scm.com/)、[Go](https://go.dev/) 和 [Dart Sass](https://gohugo.io/hugo-pipes/transpile-sass-to-css/#dart-sass)。

* 需要 Git 才能：
	* 从源代码构建 Hugo
	* 使用 Hugo 模块功能
	* 将主题安装为 Git 子模块
	* 从本地 Git 存储库访问提交信息
	* 使用 CloudCannon、Cloudflare Pages、GitHub Pages、GitLab Pages 和 Netlify 等服务托管您的网站

* Go 是必需的：
	* 从源代码构建 Hugo
	* 使用 Hugo 模块功能

* 使用 Sass 语言的最新功能时，需要 Dart Sass 将 Sass 转译为 CSS。

* 有关安装说明，请参阅相关文档：
	* [Git](https://git-scm.com/)
	* [Go](https://go.dev/) 
	* [Dart Sass](https://gohugo.io/hugo-pipes/transpile-sass-to-css/#dart-sass)。


安装方法一：预构建的二进制文件

预构建的二进制文件可用于各种操作系统和体系结构。访问[最新版本](https://github.com/gohugoio/hugo/releases/latest)页面，然后向下滚动到“资产”部分。
1. 下载所需版本、操作系统和体系结构的存档
2. 提取存档
3. 将可执行文件移动到所需的目录
4. 将此目录添加到 PATH 环境变量中
5. 验证您是否对文件具有执行权限

如果您需要有关设置文件权限或修改 PATH 环境变量的帮助，请参阅操作系统文档。

安装方法二：如果您没有看到所需版本、操作系统和体系结构的预构建二进制文件，请使用下面描述的方法之一安装 Hugo。

包管理器安装
Snap
Snap 是适用于 Linux 的免费开源包管理器。快照包适用于大多数发行版，安装简单且会自动更新。

Hugo snap 包受到严格限制。严格限制的快照在完全隔离的情况下运行，最高可达被认为始终安全的最低访问级别。您创建和构建的网站必须位于主目录中或可移动媒体上。

要安装 Hugo 的扩展版本：
```
sudo snap install hugo
```
要启用或撤消对可移动媒体的访问权限：
```
sudo snap connect hugo:removable-media
sudo snap disconnect hugo:removable-media
```
要启用或撤消对 SSH 密钥的访问权限，请执行以下操作：
```
sudo snap connect hugo:ssh-keys
sudo snap disconnect hugo:ssh-keys
```
Homebrew
Homebrew 是适用于 macOS 和 Linux 的免费开源包管理器。要安装 Hugo 的扩展版本：
```
brew install hugo
```
存储库包
大多数 Linux 发行版都为常用安装的应用程序维护一个存储库。

> 软件包存储库中提供的 Hugo 版本因 Linux 发行版和发布而异，在某些情况下不会是最新版本。
> 
> 如果您的软件包存储库未提供所需的版本，请使用其他安装方法之一。

Alpine Linux
要在 Alpine Linux 上安装 Hugo 的扩展版本：
```
doas apk add --no-cache --repository=https://dl-cdn.alpinelinux.org/alpine/edge/community hugo
```
Arch Linux
Linux 的 Arch Linux 发行版的衍生产品包括 EndeavourOS、Garuda Linux、Manjaro 等。要安装 Hugo 的扩展版本：
```
sudo pacman -S hugo
```
Debian 
Linux 的 Debian 发行版的衍生产品包括 elementary OS、KDE neon、Linux Lite、Linux Mint、MX Linux、Pop！_OS、Ubuntu、Zorin OS 等。要安装 Hugo 的扩展版本：
```
sudo apt install hugo
```
您也可以从最新版本页面下载 Debian 软件包。

Exherbo
要在 Exherbo 上安装 Hugo 的扩展版本：

1. 将此行添加到 `/etc/paludis/options.conf` 中：
```
www-apps/hugo extended
```
2. 使用 Paludis 包管理器进行安装：
```
cave resolve -x repository/heirecka
cave resolve -x hugo
```
Fedora
Linux 的 Fedora 发行版的衍生产品包括 CentOS、Red Hat Enterprise Linux 等。要安装 Hugo 的扩展版本：
```
sudo dnf install hugo
```
Gentoo
Linux的Gentoo发行版的衍生产品包括Calculate Linux、Funtoo等。要安装 Hugo 的扩展版本：

1. 在 /etc/portage/package.use/hugo 中指定 USE 标志：extended
```
www-apps/hugo extended
```
2. 使用Portage包管理器进行构建：
```
sudo emerge www-apps/hugo
```
openSUSE
Linux 的 openSUSE 发行版的衍生产品包括 GeckoLinux、Linux Karmada 等。要安装 Hugo 的扩展版本：
```
sudo zypper install hugo
```
Solus
Linux 的 Solus 发行版在其软件包存储库中包含了 Hugo。要安装 Hugo 的扩展版本：
```
sudo eopkg install hugo
```
从源代码构建
要从源代码构建 Hugo 的扩展版本，您必须：

1. 安装 Git
2. 安装 Go 版本 1.20 或更高版本
3. 安装 C 编译器，GCC 或 Clang
4. 按照 Go 文档中的说明更新 `PATH` 环境变量
> 安装 目录由 `GOPATH`  和 `GOBIN` 环境变量控制。如果设置 `GOBIN` ，则二进制文件将安装到该目录。如果设置 `GOPATH`  ，则二进制文件将安装到 `GOPATH`  列表中第一个目录的 bin 子目录中。否则，二进制文件将安装到默认 `GOPATH`   （ `$HOME/go` 或 `%USERPROFILE%\go` ） 的 bin 子目录中。

然后构建并测试：
```
CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@latest
hugo version
```
各安装方法比较
|      功能      | 预构建的二进制文件 | 包管理器 | 存储库包 | 从源代码构建 |
| :------------: | :----------------: | :------: | :------: | :----------: |
|   易于安装？   |         ✔️          |    ✔️     |    ✔️     |      ✔️       |
|   易于升级？   |         ✔️          |    ✔️     |   不同   |      ✔️       |
|   容易降级？   |         ✔️          |  ✔️[^1]   |   不同   |      ✔️       |
|   自动更新？   |         ❌          | 不同[^2] |    ❌     |      ❌       |
| 有最新版本吗？ |         ✔️          |    ✔️     |   不同   |      ✔️       |

[^1]: 如果仍安装以前的版本，则很容易。

[^2]: Snap 软件包会自动更新。Homebrew 需要高级配置。


## 安装步骤

1. 添加 epel repo，/etc/yum.repos.d/hugo.repo
```
[root@192 ~]# vim /etc/yum.repos.d/hugo.repo

# 在其中添加以下内容：

[daftaupe-hugo]
name=Copr repo for hugo owned by daftaupe
baseurl=https://copr-be.cloud.fedoraproject.org/results/daftaupe/hugo/epel-7-$basearch/
type=rpm-md
skip_if_unavailable=True
gpgcheck=1
gpgkey=https://copr-be.cloud.fedoraproject.org/results/daftaupe/hugo/pubkey.gpg
repo_gpgcheck=0
enabled=1
```
2. 执行安装 hugo 命令 `yum -y install hugo`

```
[root@192 ~]# yum install hugo
已加载插件：fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.nju.edu.cn
 * extras: mirrors.nju.edu.cn
 * updates: mirrors.nju.edu.cn
daftaupe-hugo                                                                                    | 1.8 kB  00:00:00
daftaupe-hugo/x86_64/primary                                                                     | 1.1 kB  00:00:16
daftaupe-hugo                                                                                                       2/2
正在解决依赖关系
--> 正在检查事务
---> 软件包 hugo.x86_64.0.0.123.8-1.el7 将被 安装
--> 解决依赖关系完成

依赖关系解决

========================================================================================================================
 Package                架构                     版本                             源                               大小
========================================================================================================================
正在安装:
 hugo                   x86_64                   0.123.8-1.el7                    daftaupe-hugo                    17 M

事务概要
========================================================================================================================
安装  1 软件包

总下载量：17 M
安装大小：87 M
Is this ok [y/d/N]: y
Downloading packages:
警告：/var/cache/yum/x86_64/7/daftaupe-hugo/packages/hugo-0.123.8-1.el7.x86_64.rpm: 头V4 RSA/SHA256 Signature, 密钥 ID 47eace92: NOKEY
hugo-0.123.8-1.el7.x86_64.rpm 的公钥尚未安装
hugo-0.123.8-1.el7.x86_64.rpm                                                                    |  17 MB  00:00:19
从 https://copr-be.cloud.fedoraproject.org/results/daftaupe/hugo/pubkey.gpg 检索密钥
导入 GPG key 0x47EACE92:
 用户ID     : "daftaupe_Hugo (None) <daftaupe#Hugo@copr.fedorahosted.org>"
 指纹       : 5aeb a78b 481d ed48 16ed b902 fdea 18c5 47ea ce92
 来自       : https://copr-be.cloud.fedoraproject.org/results/daftaupe/hugo/pubkey.gpg
是否继续？[y/N]：y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : hugo-0.123.8-1.el7.x86_64                                                                           1/1
  验证中      : hugo-0.123.8-1.el7.x86_64                                                                           1/1

已安装:
  hugo.x86_64 0:0.123.8-1.el7

完毕！
```

3. 查看版本 `hugo version`

```
[root@192 ~]# hugo version
hugo v0.123.8+extended linux/amd64 BuildDate=unknown VendorInfo=mage
```

这样装的hugo版本不是最新版本，所以还是建议官网下下载安装。

4. 下载：[下载Hugo](https://github.com/gohugoio/hugo/releases)
```
[root@192 ~]# wget https://github.com/gohugoio/hugo/releases/download/v0.125.4/hugo_extended_0.125.4_linux-amd64.tar.gz
--2024-04-27 15:01:19--  https://github.com/gohugoio/hugo/releases/download/v0.125.4/hugo_extended_0.125.4_linux-amd64.tar.gz
正在解析主机 github.com (github.com)... 20.205.243.166
正在连接 github.com (github.com)|20.205.243.166|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 302 Found
长度：22089284 (21M) [application/octet-stream]
正在保存至: “hugo_extended_0.125.4_linux-amd64.tar.gz”

100%[===============================================================================================>] 22,089,284   262KB/s 用时 1m 54s 

2024-04-27 15:04:18 (189 KB/s) - 已保存 “hugo_extended_0.125.4_linux-amd64.tar.gz” [22089284/22089284])
```

下载完成后接着解压到指定的文件夹，先在服务器上创建一个解压后的文件夹，如：/usr/local/hugo

```
[root@192 ~]# cd /usr/local
[root@192 local]# mkdir hugo
[root@192 go]# cd ~
[root@192 ~]# tar -C /usr/local/hugo/ -zxvf hugo_extended_0.125.4_linux-amd64.tar.gz
hugo
README.md
LICENSE
```
解压后，文件夹中就会有个hugo绿色的文件，就是hugo的执行程序。
```
[root@192 ~]# cd /usr/local/hugo/
[root@192 hugo]# ll
总用量 83664
-rwxr-xr-x. 1 root root 85640840 4月  25 21:33 hugo
-rw-r--r--. 1 root root    11357 4月  25 21:26 LICENSE
-rw-r--r--. 1 root root    12891 4月  25 21:26 README.md
```

复制一份hugo程序到/usr/local/bin/：
`cp ./hugo /usr/local/bin/`  不然hugo执行找不到路径
```
[root@19``2 hugo]# cp ./hugo /usr/local/bin/
[root@192 hugo]# hugo version
hugo v0.123.8+extended linux/amd64 BuildDate=unknown VendorInfo=mage
### 执行 hugo 程序没变化，这个办法没有用。

[root@192 hugo]# ./hugo version
./hugo: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by ./hugo)
./hugo: /lib64/libstdc++.so.6: version `CXXABI_1.3.8' not found (required by ./hugo)
./hugo: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by ./hugo)
### 下载解压出来的 hugo 程序关联文件版本也出错，这个方法不可行。
```

生成站点，也可以指定其他路径生成，path表示要安装的路径，如：/usr/local/hugo

`hugo new site path`

