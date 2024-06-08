---
title: "建立小站的第一天"
description: "记录一下建站的过程"
# linkTitle:
date: 2024-04-07T16:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 1
nav_icon:
  vendor: bootstrap
  name: intersect
  color: SkyBlue
series:
  - Mkdocs
categories:
  - 笔记
tags:
  - Windows
  - Mkdocs
images:
  - https://s2.loli.net/2024/05/11/cfskg6xm4duv3UN.jpg?width=1920&height=1440
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

# 建立小站的第一天

* 记录一下建站的过程。
这个是我最早学习用 Mkdocs 搭建静态网站。也从此开始了 IT 学习之路。

## 参考内容

* 全篇参考了以下内容：
* [【轻编程】B站视频：Python版宝藏级静态站点生成器Material for MkDocs](https://www.bilibili.com/video/BV1nt4y157sR/)
* [【正月点灯笼】B站视频：用python和mkdocs制作简易个人网站](https://www.bilibili.com/video/BV1JW411p7Tw/)
* [【Material for MkDocs】网站](https://squidfunk.github.io/mkdocs-material/)
* [启动venv虚拟环境报错，参考【Alex_81D】的帖子：win10启动venv报错：无法加载文件 venv\Scripts\activate.ps1，因为在此系统上禁止运行脚本。](https://blog.csdn.net/Alex_81D/article/details/133904929)

## 具体步骤

### 前提

* 在Win11系统里已经有了Visual Studio Code。
* 本机 Python 版本 `python -V` - Python 3.12.2
* 本机原 pip 版本 `pip -V` - pip 23.2.1

### 安装Mkdocs

* 1、在Win11文档内新建DOC文件夹
* 2、启动VS code打开DOC文件夹
* 3、在VS code中新建终端，然后创建虚拟环境

#### 创建虚拟环境
```
    py -m venv venv         # 创建虚拟环境
    venv\Scripts\activate   # 激活虚拟环境
    venv\Scripts\activate : 无法加载文件 C:\Users……  # 报错
```
```
    ## 上网站搜索，解决报错问题
    get-executionpolicy     # VS code终端输入get-executionpolicy，回车返回Restricted。
    Start-Process powershell -Verb runAs # 打开 windows powershell，输入Start-Process powershell -Verb runAs 进入管理员模式
    set-executionpolicy remotesigned     # 再输入set-executionpolicy remotesigned，回车，输入Y
    get-executionpolicy     # VS code终端再次输入get-executionpolicy，命令回车，返回remotesigned。
    \venv\Scripts\activate  # 回车，进入虚拟环境，解决。
```
### 继续安装Mkdocs

* 4、按照Material for MkDocs网站中Getting started文档继续操作
  
    `pip install mkdocs-material` - 安装mkdocs-material

* 5、安装程序提醒我升级pip
  
    `python.exe -m pip install --upgrade pip` - 升级pip

* 6、用mkdocs新建一个网站项目
* 
    `mkdocs new mysite` - 使用命令 mkdocs new XXX 创建自己的项目

* 7、启动mkdocs服务器
* 
    `cd mysite` - 进入项目所在文件夹 
    `mkdocs serve` - 使用命令 mkdocs serve启动服务，默认 http://localhost:8000/ 可浏览效果

    注：新建项目默认结构
```
mkdocs.yml    # 配置文件。
docs/         # 存放站点文件
index.md      # 文档主页。
...           # 其他 markdown 页面、图像和其他文件。
```
* 8、My docs常用命令

    `mkdocs new XXX` - 创建自己的XXX项目。

    `mkdocs serve` - 启动实时重新加载文档服务器。

    `mkdocs build` - 建立文档网站。

    `mkdocs -h` - 打印帮助信息并退出。

### 参考官网对各功能设置

* 参考 [【Material for MkDocs】](https://squidfunk.github.io/mkdocs-material/setup/)Setup页面
* 在 mkdocs.yml 文件中设置各模块功能
* 在 /docs/index.md 文件中写网站内容

#### 设置主题颜色

* 将下面的代码复制粘贴到 mkdocs.yml 文件内，层级与 “site_name: 菜鸟小站” 同一级别。
```
        theme:
            palette: 

            # Palette toggle for light mode
            - scheme: default
                toggle:
                    icon: material/brightness-7 
                    name: Switch to dark mode

                # Palette toggle for dark mode
                - scheme: slate
                    toggle:
                        icon: material/brightness-4
                        name: Switch to light mode
```
#### 设置站点语言为中文
* 将下面的代码复制粘贴到 mkdocs.yml 文件内，参考 “theme:” 字段，设置好层级关系。
```
        theme:
            language: zh
```
#### 设置网站菜单结构

* 1、在 mkdocs.yml 文件中添加以下代码
```
        site_name: 菜鸟小站

        nav:
            - 主页:
                - index.md 
            - 建站记录:
                - build-site/note.md
                - build-site/page-1.md
                - build-site/page-2.md
```
* 2、在 mysite 文件夹下新建以下文件：
```
        mkdocs.yml    # 配置文件。
        docs/
            build-site/
                note.md
                page-1.md
                page-2.md
            index.md  # 文档主页。
```
* 3、在 mkdocs.yml 文件中添加以下导航模块代码
```
        theme:
            features:
                - navigation.tabs
                - navigation.tabs.sticky
                - navigation.sections
                - navigation.indexes
                - navigation.instant
                - navigation.instant.progress
                - navigation.tracking
                - navigation.path
                - toc.integrate
                - navigation.top
                - header.autohide
                - announce.dismiss
            name: material
```
#### 设置网站页脚

* 1、页脚可以包含指向当前页面的上一页和下一页的链接。如果要启用此行为，请将以下行添加到：mkdocs.yml
    
    我没有开启此功能
```
        theme:
            features:
                - navigation.footer
```
* 2、社交链接作为项目文档页脚的一部分呈现在版权声明旁边。添加社交链接列表：mkdocs.yml
```
        extra:
            social:
                - icon: fontawesome/brands/docker
                    link: https://fosstodon.org/@squidfunk
```
* 3、版权声明：自定义版权横幅可以呈现为页脚的一部分，页脚显示在社交链接旁边。它可以定义为以下部分：mkdocs.yml
```
        copyright: Copyright &copy; 2016 - 2020 Martin Donath
```
* 4、页脚显示“Made with Material for MkDocs”通知，以指示网站的生成方式。可以通过以下选项删除通知：mkdocs.yml
```
        extra:
            generator: false
```
## 至此，建立该网站暂告一段落

* 剩余的就是把内容写好了。
