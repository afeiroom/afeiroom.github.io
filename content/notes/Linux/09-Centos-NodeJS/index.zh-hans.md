---
title: CentOS7 安装 NodeJS 详细教程
description: "官网下载 .tar.gz 手动安装，并解决报错问题。"
# linkTitle:
date: 2024-04-27T02:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 9
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
  - NodeJS
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

# CentOS7 安装NodeJS详细教程

  　　————2024.4.27

## 参考链接
* [warton88【centos 安装Nodejs v20.11.1】](https://blog.csdn.net/warton88/article/details/136869882)

* [林仔520【CentOS7 安装NodeJS详细教程（附带安装步骤）】](https://blog.csdn.net/qq_37955704/article/details/113395046)
## 1. 下载nodejs压缩包
国内官网下载链接：http://nodejs.cn/download/

官方网站下载链接：https://nodejs.org/en/download

执行下载命令：`wget https://nodejs.org/dist/v20.12.2/node-v20.12.2-linux-x64.tar.xz`
```
[root@192 ~]# wget https://nodejs.org/dist/v20.12.2/node-v20.12.2-linux-x64.tar.xz
--2024-04-27 16:57:12--  https://nodejs.org/dist/v20.12.2/node-v20.12.2-linux-x64.tar.xz
正在解析主机 nodejs.org (nodejs.org)... 2606:4700:10::6814:172e, 2606:4700:10::6814:162e, 104.20.22.46, ...
正在连接 nodejs.org (nodejs.org)|104.20.22.46|:443... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：25710972 (25M) [application/x-xz]
正在保存至: “node-v20.12.2-linux-x64.tar.xz”

100%[==============================================================================>] 25,710,972  6.71MB/s 用时 3.7s

2024-04-27 17:01:31 (6.71 MB/s) - 已保存 “node-v20.12.2-linux-x64.tar.xz” [25710972/25710972])
```

## 2. 解压缩
执行以下命令：
```
tar -xvf node-v14.15.4-linux-x64.tar.xz
mkdir -p /usr/local/nodejs
mv node-v14.15.4-linux-x64/* /usr/local/nodejs/
```

```
[root@192 ~]# tar -xvf node-v20.12.2-linux-x64.tar.xz
node-v20.12.2-linux-x64/
node-v20.12.2-linux-x64/bin/
node-v20.12.2-linux-x64/bin/corepack
node-v20.12.2-linux-x64/bin/npx
node-v20.12.2-linux-x64/bin/node
node-v20.12.2-linux-x64/bin/npm
node-v20.12.2-linux-x64/include/
node-v20.12.2-linux-x64/include/node/
……………………
node-v20.12.2-linux-x64/lib/node_modules/npm/LICENSE
node-v20.12.2-linux-x64/LICENSE

[root@192 ~]# mkdir -p /usr/local/nodejs

[root@192 ~]# mv node-v20.12.2-linux-x64/* /usr/local/nodejs/
```


```
### 备注：mkdir [-p] dirName
### 参数说明：-p 可以一次性创建多重目录
一次性创建多重目录
```


## 3. 创建软链接

执行下面2条命令：
```
# 建立node软链接
ln -s /usr/local/nodejs/bin/node /usr/local/bin
# 建立npm 软链接
ln -s /usr/local/nodejs/bin/npm /usr/local/bin
# 建立npx 软链接
ln -s /usr/local/nodejs/bin/npx /usr/local/bin

```

```
[root@192 nodejs]# ln -s /usr/local/nodejs/bin/node /usr/local/bin
[root@192 nodejs]# ln -s /usr/local/nodejs/bin/npm /usr/local/bin
[root@192 nodejs]# ls /usr/local/bin -a
.  ..  hugo  node  npm
```

## 出现报错，解决问题
```
[root@192 ~]# node
node: /lib64/libm.so.6: version `GLIBC_2.27' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by node)
node: /lib64/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by node)
node: /lib64/libc.so.6: version `GLIBC_2.28' not found (required by node)
node: /lib64/libc.so.6: version `GLIBC_2.25' not found (required by node)
```

以上报错，缺少相关动态库。

### 1. 升级gcc
```
$ yum update

# 升级GCC(默认为4 升级为8)
$ yum install -y centos-release-scl
$ yum install -y devtoolset-8-gcc*
$ mv /usr/bin/gcc /usr/bin/gcc-4.8.5
$ ln -s /opt/rh/devtoolset-8/root/bin/gcc /usr/bin/gcc
$ mv /usr/bin/g++ /usr/bin/g++-4.8.5
$ ln -s /opt/rh/devtoolset-8/root/bin/g++ /usr/bin/g++
 
# 升级 make(默认为3 升级为4)
$ wget http://ftp.gnu.org/gnu/make/make-4.3.tar.gz
$ tar -xzvf make-4.3.tar.gz && cd make-4.3/
$ ./configure  --prefix=/usr/local/make
$ make && make install
$ cd /usr/bin/ && mv make make.bak
$ ln -sv /usr/local/make/bin/make /usr/bin/make
 
#验证gcc版本
$ gcc -v
```

```
[root@192 bin]# gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/opt/rh/devtoolset-8/root/usr/libexec/gcc/x86_64-redhat-linux/8/lto-wrapper
Target: x86_64-redhat-linux
Configured with: ../configure --enable-bootstrap --enable-languages=c,c++,fortran,lto --prefix=/opt/rh/devtoolset-8/root/usr --mandir=/opt/rh/devtoolset-8/root/usr/share/man --infodir=/opt/rh/devtoolset-8/root/usr/share/info --with-bugurl=http://bugzilla.redhat.com/bugzilla --enable-shared --enable-threads=posix --enable-checking=release --enable-multilib --with-system-zlib --enable-__cxa_atexit --disable-libunwind-exceptions --enable-gnu-unique-object --enable-linker-build-id --with-gcc-major-version-only --with-linker-hash-style=gnu --with-default-libstdcxx-abi=gcc4-compatible --enable-plugin --enable-initfini-array --with-isl=/builddir/build/BUILD/gcc-8.3.1-20190311/obj-x86_64-redhat-linux/isl-install --disable-libmpx --enable-gnu-indirect-function --with-tune=generic --with-arch_32=x86-64 --build=x86_64-redhat-linux
Thread model: posix
gcc version 8.3.1 20190311 (Red Hat 8.3.1-3) (GCC)
```

升级 glibc-2.28
```
$ cd ~
$ wget http://ftp.gnu.org/gnu/glibc/glibc-2.28.tar.gz
$ tar xf glibc-2.28.tar.gz 
$ cd glibc-2.28/ && mkdir build  && cd build
$ ../configure --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin --enable-obsolete-nsl
$ make -j 10
$ make localedata/install-locales -j 10
$ make install -j 10
```

遇到错误
```
checking for python3... python3
configure: error:
*** These critical programs are missing or too old: bison
*** Check the INSTALL file for required versions.
```
解决办法
```
 $ yum install bison
 
 # 安装后执行安装glibc
 
 # 再次遇到错误
/usr/bin/ld: cannot find -lnss_test2
collect2: error: ld returned 1 exit status
Execution of gcc -B/usr/bin/ failed!
The script has found some problems with your installation!
Please read the FAQ and the README file and check the following:
- Did you change the gcc specs file (necessary after upgrading from
  Linux libc5)?
- Are there any symbolic links of the form libXXX.so to old libraries?
  Links like libm.so -> libm.so.5 (where libm.so.5 is an old library) are wrong,
  libm.so should point to the newly installed glibc file - and there should be
  only one such link (check e.g. /lib and /usr/lib)
You should restart this script from your build directory after you've
fixed all problems!
Btw. the script doesn't work if you're installing GNU libc not as your
primary library!
make[1]: *** [Makefile:111: install] Error 1
make[1]: Leaving directory '/www/tools/glibc-2.28'
make: *** [Makefile:12: install] Error 2
```
解决办法
```
$ vim scripts/test-installation.pl
```
在文件的128行新增$name ne “nss_test2”，如下图所示：

![test-installation.png](https://s2.loli.net/2024/06/11/poFP5WuDl16vdrk.png)

重新执行glibc安装命令，可顺利安装，然后校验
```
$ node -V
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by node)
node: /lib64/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by node)
```
仍有部分报错需要解决，出现 `/usr/lib64/libstdc++.so.6: version 'GLIBCXX_3.4.20' not found` 的问题，是因为生成的动态库没有替换老版本gcc的动态库导致的。将gcc最新版本的动态库替换系统中老版本的动态库即可解决。
```
# 先试用yum版本，看看能否解决问题，如果不能解决问题，用后面方法。
$ strings /usr/lib64/libstdc++.so.6 | grep GLIBCXX
$ strings /lib64/libstdc++.so.6 | grep GLIBCXX
 
$ yum whatprovides libstdc++.so.6
$ yum update -y libstdc++.x86_64
 
 
# 下载稍微新一点的版本
sudo wget http://www.vuln.cn/wp-content/uploads/2019/08/libstdc.so_.6.0.26.zip
unzip libstdc.so_.6.0.26.zip
cp libstdc++.so.6.0.26 /lib64/
cd /lib64
 
# 把原来的命令做备份
cp libstdc++.so.6 libstdc++.so.6.bak
rm -f libstdc++.so.6
 
# 重新链接
ln -s libstdc++.so.6.0.26 libstdc++.so.6
```



## 4. 更换镜像源

```
# 设置国内镜像源
npm config set registry https://registry.npmmirror.com
# 查看设置信息
npm config list
```

```
[root@192 ~]# npm config set registry https://registry.npmmirror.com
[root@192 ~]# npm config list
; "user" config from /root/.npmrc

registry = "https://registry.npmmirror.com"

; node bin location = /usr/local/nodejs/bin/node
; node version = v20.12.2
; npm local prefix = /root
; npm version = 10.5.0
; cwd = /root
; HOME = /root
; Run `npm config ls -l` to show all defaults.
```


## 5. 验证是否安装成功
node -v
npm -v

```
[root@192 ~]# node --version
v20.12.2
[root@192 ~]# npm --version
10.5.0
```

