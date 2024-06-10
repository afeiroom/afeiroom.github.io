---
title: CentOS7 升级 Git （最新方法，秒杀一切旧方法！）
description: "使用 IUS 安装，该方法也是 Git 官方推荐的。"
# linkTitle:
date: 2024-05-06T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 10
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
  - Git
  - IUS
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

# CentOS7 升级 Git （最新方法，秒杀一切旧方法！）

  　　————2024.5.6

使用 IUS 安装，该方法也是 Git 官方推荐的。

RHEL 及其衍生产品（包括 CentOS ）通常会优先考虑安全性和稳定性，而不是添加新功能。这构造了一个安全且稳定的操作系统，但有时用户愿意牺牲一些稳定性，以便获得较新软件版本中的功能。
## 参考链接

[HinGwenWoong 【CentOS7 升级 Git （最新方法，秒杀一切旧方法！）】](https://blog.csdn.net/hxj0323/article/details/119751427)

## 操作步骤

### 1. 卸载旧版本的Git
```
yum remove git
```

执行以下命令：
```
[root@192 ~]# yum remove git
已加载插件：fastestmirror, langpacks
正在解决依赖关系
--> 正在检查事务
---> 软件包 git.x86_64.0.1.8.3.1-25.el7_9 将被 删除
--> 正在处理依赖关系 git = 1.8.3.1-25.el7_9，它被软件包 perl-Git-1.8.3.1-25.el7_9.noarch 需要
--> 正在检查事务
---> 软件包 perl-Git.noarch.0.1.8.3.1-25.el7_9 将被 删除
--> 解决依赖关系完成

依赖关系解决

===================================================================
 Package      架构       版本                   源            大小
===================================================================
正在删除:
 git          x86_64     1.8.3.1-25.el7_9       @updates      22 M
为依赖而移除:
 perl-Git     noarch     1.8.3.1-25.el7_9       @updates      57 k

事务概要
===================================================================
移除  1 软件包 (+1 依赖软件包)

安装大小：22 M
是否继续？[y/N]：y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在删除    : perl-Git-1.8.3.1-25.el7_9.noarch               1/2 
  正在删除    : git-1.8.3.1-25.el7_9.x86_64                    2/2 
  验证中      : git-1.8.3.1-25.el7_9.x86_64                    1/2 
  验证中      : perl-Git-1.8.3.1-25.el7_9.noarch               2/2 

删除:
  git.x86_64 0:1.8.3.1-25.el7_9                                    

作为依赖被删除:
  perl-Git.noarch 0:1.8.3.1-25.el7_9                               

完毕！
```


### 2. 安装 IUS：

RHEL/CentOS 7 操作系统
```
yum install \
https://repo.ius.io/ius-release-el7.rpm \
https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```


执行以下命令（因连接外网不稳定，执行了很多次才成功）：
```
[root@192 ~]# yum install https://repo.ius.io/ius-release-el7.rpm https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
已加载插件：fastestmirror, langpacks
ius-release-el7.rpm                         | 8.2 kB     00:00     
正在检查 /var/tmp/yum-root-FJrPhY/ius-release-el7.rpm: ius-release-2-1.el7.ius.noarch
/var/tmp/yum-root-FJrPhY/ius-release-el7.rpm 将被安装
epel-release-latest-7.noarch.rpm            |  15 kB     00:00     
正在检查 /var/tmp/yum-root-FJrPhY/epel-release-latest-7.noarch.rpm: epel-release-7-14.noarch
/var/tmp/yum-root-FJrPhY/epel-release-latest-7.noarch.rpm 将被安装
正在解决依赖关系
--> 正在检查事务
---> 软件包 epel-release.noarch.0.7-14 将被 安装
---> 软件包 ius-release.noarch.0.2-1.el7.ius 将被 安装
--> 解决依赖关系完成

依赖关系解决

===================================================================
 Package      架构   版本      源                             大小
===================================================================
正在安装:
 epel-release noarch 7-14      /epel-release-latest-7.noarch  25 k
 ius-release  noarch 2-1.el7.ius
                               /ius-release-el7              4.5 k

事务概要
===================================================================
安装  2 软件包

总计：30 k
安装大小：30 k
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : epel-release-7-14.noarch                       1/2 
  正在安装    : ius-release-2-1.el7.ius.noarch                 2/2 
  验证中      : epel-release-7-14.noarch                       1/2 
  验证中      : ius-release-2-1.el7.ius.noarch                 2/2 

已安装:
  epel-release.noarch 0:7-14    ius-release.noarch 0:2-1.el7.ius   

完毕！
```

### 3. 去到 IUS 的 [Github repo](https://github.com/search?q=org%3Aiusrepo+topic%3Arpm&s=updated&type=repositories) 查看需要的库和版本：

我这里搜索到的是 Git 2.36
```
iusrepo/git236
Fast Version Control System
rpm·hacktoberfest
Shell·13·Updated on 2023年5月3日
```


### 4. 去到 CentOS 在命令行直接敲：
```
yum install git224
```

执行以下命令：
```
[root@192 ~]# yum install git236
已加载插件：fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.nju.edu.cn
 * centos-sclo-rh: mirrors.nju.edu.cn
 * centos-sclo-sclo: mirrors.huaweicloud.com
 * epel: mirrors.bfsu.edu.cn
 * extras: mirrors.nju.edu.cn
 * updates: mirrors.nju.edu.cn
base                                        | 3.6 kB     00:00     
centos-sclo-rh                              | 3.0 kB     00:00     
centos-sclo-sclo                            | 3.0 kB     00:00     
daftaupe-hugo                               | 1.8 kB     00:00     
extras                                      | 2.9 kB     00:00     
ius                                         | 1.3 kB     00:00     
updates                                     | 2.9 kB     00:00     
ius/x86_64/primary                            |  40 kB   00:23     
ius                                                        159/159
正在解决依赖关系
--> 正在检查事务
---> 软件包 git236.x86_64.0.2.36.6-1.el7.ius 将被 安装
--> 正在处理依赖关系 perl-Git = 2.36.6-1.el7.ius，它被软件包 git236-2.36.6-1.el7.ius.x86_64 需要
--> 正在处理依赖关系 git-core-doc = 2.36.6-1.el7.ius，它被软件包 git236-2.36.6-1.el7.ius.x86_64 需要
--> 正在处理依赖关系 git-core = 2.36.6-1.el7.ius，它被软件包 git236-2.36.6-1.el7.ius.x86_64 需要
--> 正在处理依赖关系 perl(Git::I18N)，它被软件包 git236-2.36.6-1.el7.ius.x86_64 需要
--> 正在处理依赖关系 perl(Git)，它被软件包 git236-2.36.6-1.el7.ius.x86_64 需要
--> 正在检查事务
---> 软件包 git236-core.x86_64.0.2.36.6-1.el7.ius 将被 安装
---> 软件包 git236-core-doc.noarch.0.2.36.6-1.el7.ius 将被 安装
---> 软件包 git236-perl-Git.noarch.0.2.36.6-1.el7.ius 将被 安装
--> 解决依赖关系完成

依赖关系解决

===================================================================
 Package             架构       版本                 源       大小
===================================================================
正在安装:
 git236              x86_64     2.36.6-1.el7.ius     ius      71 k
为依赖而安装:
 git236-core         x86_64     2.36.6-1.el7.ius     ius     6.9 M
 git236-core-doc     noarch     2.36.6-1.el7.ius     ius     2.8 M
 git236-perl-Git     noarch     2.36.6-1.el7.ius     ius      46 k

事务概要
===================================================================
安装  1 软件包 (+3 依赖软件包)

总下载量：9.7 M
安装大小：40 M
Is this ok [y/d/N]: y
Downloading packages:
警告：/var/cache/yum/x86_64/7/ius/packages/git236-2.36.6-1.el7.ius.x86_64.rpm: 头V4 RSA/SHA256 Signature, 密钥 ID 4b274df2: NOKEY
git236-2.36.6-1.el7.ius.x86_64.rpm 的公钥尚未安装
(1/4): git236-2.36.6-1.el7.ius.x86_64.rpm     |  71 kB   00:23     
(2/4): git236-core-2.36.6-1.el7.ius.x86_64.rp | 6.9 MB   00:24     
(3/4): git236-core-doc-2.36.6-1.el7.ius.noarc | 2.8 MB   00:01     
(4/4): git236-perl-Git-2.36.6-1.el7.ius.noarc |  46 kB   00:00     
-------------------------------------------------------------------
总计                                  398 kB/s | 9.7 MB  00:25     
从 file:///etc/pki/rpm-gpg/RPM-GPG-KEY-IUS-7 检索密钥
导入 GPG key 0x4B274DF2:
 用户ID     : "IUS (7) <dev@ius.io>"
 指纹       : c958 7a09 a11f d706 4f0c a0f4 e558 0725 4b27 4df2
 软件包     : ius-release-2-1.el7.ius.noarch (@/ius-release-el7)
 来自       : /etc/pki/rpm-gpg/RPM-GPG-KEY-IUS-7
是否继续？[y/N]：y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : git236-core-2.36.6-1.el7.ius.x86_64            1/4 
  正在安装    : git236-core-doc-2.36.6-1.el7.ius.noarch        2/4 
  正在安装    : git236-perl-Git-2.36.6-1.el7.ius.noarch        3/4 
  正在安装    : git236-2.36.6-1.el7.ius.x86_64                 4/4 
  验证中      : git236-2.36.6-1.el7.ius.x86_64                 1/4 
  验证中      : git236-core-doc-2.36.6-1.el7.ius.noarch        2/4 
  验证中      : git236-perl-Git-2.36.6-1.el7.ius.noarch        3/4 
  验证中      : git236-core-2.36.6-1.el7.ius.x86_64            4/4 

已安装:
  git236.x86_64 0:2.36.6-1.el7.ius                                 

作为依赖被安装:
  git236-core.x86_64 0:2.36.6-1.el7.ius                            
  git236-core-doc.noarch 0:2.36.6-1.el7.ius                        
  git236-perl-Git.noarch 0:2.36.6-1.el7.ius                        

完毕！
```


### 5. 检查安装版本

```
git version
```

执行以下命令：
```
[root@192 ~]# git version
git version 2.36.6
```

安装成功！