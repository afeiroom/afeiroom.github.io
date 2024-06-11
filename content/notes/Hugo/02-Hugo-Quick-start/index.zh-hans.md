---
title: Hugo快速入门
description: "学习创建一个 Hugo 网站。"
# linkTitle:
date: 2024-04-20T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 2
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
  - 创建网站
  - Windows
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

# Hugo快速入门（Windows）


学习在几分钟内创建一个 Hugo 网站。
在本教程中，您将：
> 创建站点
> 添加内容
> 配置站点
> 发布网站
> 先决条件

## 参考内容

* [Hugo官网 Quick start](https://gohugo.io/getting-started/quick-start/)
* [Stack主题官网说明 Getting Started](https://stack.jimmycai.com/guide/getting-started)

##  在开始本教程之前，必须

* 安装 Hugo（扩展版，v0.112.0 或更高版本）
* 安装 Git
* 您还必须能够自如地从命令行工作。

## 创建站点

> 如果您是 Windows 用户：
> * 不要使用命令提示符
> * 不要使用 Windows PowerShell
> * 从 PowerShell 或 Linux 终端（如 WSL 或 Git Bash）运行这些命令
PowerShell 和 Windows PowerShell 是不同的应用程序。

验证您是否已安装 Hugo v0.112.0 或更高版本。`hugo version`
```
c:\hugo\Sites\afeiroom>hugo version
hugo v0.125.1-68c5ad638c2072969e47262926b912e80fd71a77+extended windows/amd64 BuildDate=2024-04-18T08:21:19Z VendorInfo=gohugoio
```

运行这些命令以创建具有 stack 主题的 Hugo 站点，站点名称为 afeiroom。

```
c:\hugo\Sites>hugo new site afeiroom		# 创建 afeiroom 站点项目
Congratulations! Your new Hugo site was created in c:\hugo\Sites\afeiroom.
……
c:\hugo\Sites>cd afeiroom			# 进入站点项目文件夹

c:\hugo\Sites\afeiroom>git init			# 初始化一个空的git本地仓库
Initialized empty Git repository in C:/hugo/Sites/afeiroom/.git/
```
在 master 分支上，您可以找到主题的最新源代码。要使用最新版本，您可以通过在 Hugo 站点的根目录中运行以下命令来克隆存储库：`themes/hugo-theme-stack`

**注意**：拉取主题前，先关掉 `翻墙代理`，不然 `git` 总是连接错误。

```
# stack 主题设置感觉好麻烦，暂时不用这个了！！！
c:\hugo\Sites\afeiroom>git clone https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack	# 去官网拉取stack主题
Cloning into 'themes/hugo-theme-stack'...
remote: Enumerating objects: 5065, done.
remote: Counting objects: 100% (336/336), done.
remote: Compressing objects: 100% (197/197), done.
remote: Total 5065 (delta 185), reused 245 (delta 132), pack-reused 4729
Receiving objects: 100% (5065/5065), 1.23 MiB | 2.12 MiB/s, done.
Resolving deltas: 100% (3226/3226), done.
```
如果您已经在为您的站点使用 Git，您可以通过在 Hugo 站点的根目录中运行以下命令将主题添加为子模块：
> git submodule add https://github.com/CaiJimmy/hugo-theme-stack/ themes/hugo-theme-stack

```
# 拉取 relearn z主题到站点 themes/hugo-theme-relearn 文件夹下
C:\hugo\Sites\afeiroom>git clone https://github.com/McShelby/hugo-theme-relearn.git themes/hugo-theme-relearn
Cloning into 'themes/hugo-theme-relearn'...
remote: Enumerating objects: 529211, done.
remote: Counting objects: 100% (268379/268379), done.
remote: Compressing objects: 100% (8080/8080), done.
remote: Total 529211 (delta 260515), reused 267938 (delta 260184), pack-reused 260832
Receiving objects: 100% (529211/529211), 374.98 MiB | 1.52 MiB/s, done.
Resolving deltas: 100% (326161/326161), done.

```

在站点配置文件中追加一行，指示当前主题。echo theme = 'hugo-theme-relearn' >> hugo.toml		
```
c:\hugo\Sites\afeiroom>echo theme = 'hugo-theme-relearn' >> hugo.toml
```
启动 Hugo 的开发服务器以查看站点。hugo server -D
```
c:\hugo\Sites\afeiroom>hugo server -D
Watching for changes in c:\hugo\Sites\afeiroom\{archetypes,assets,content,data,i18n,layouts,static,themes}
Watching for config changes in c:\hugo\Sites\afeiroom\hugo.toml, c:\hugo\Sites\afeiroom\themes\hugo-theme-stack\config.yaml
Start building sites …
hugo v0.125.1-68c5ad638c2072969e47262926b912e80fd71a77+extended windows/amd64 BuildDate=2024-04-18T08:21:19Z VendorInfo=gohugoio


                   | EN
-------------------+-----
  Pages            |  8
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  1
  Aliases          |  3
  Cleaned          |  0

Built in 242 ms
Environment: "development"
Serving pages from disk
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```
用浏览器打开 `http://localhost:1313/` 就可以在本地浏览默认的页面了。

按下可停止 Hugo 的开发服务器。Ctrl + C


## 添加内容
将新页面添加到您的网站。`hugo new content posts/my-first-post.md`

```
C:\hugo\Sites\afeiroom>hugo new content posts/my-first-post.md
Content "C:\\hugo\\Sites\\afeiroom\\content\\posts\\my-first-post.md" created
```

Hugo 在目录`content/posts`中创建了`my-first-post.md`文件 。使用编辑器打开该文件。
```
+++
title = 'My First Post'
date = 2024-01-14T07:07:07+01:00
draft = true
+++
```
请注意，前面的值是 `draft = true`。默认情况下，Hugo 不会在您构建网站时发布草稿内容。详细了解草稿内容、未来内容和过期内容。

在帖子正文中添加一些 Markdown，但不要更改`draft`值。
```
+++
title = 'My First Post'
date = 2024-01-14T07:07:07+01:00
draft = true
+++
## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!
```
保存文件，然后启动 Hugo 的开发服务器查看站点。您可以运行以下任一命令以包含草稿内容。
```
hugo server --buildDrafts
hugo server -D
```
在终端中显示的 URL 中查看您的站点。在继续添加和更改内容时，使开发服务器保持运行。

如果对新内容感到满意，请将 front matter 参数设置为 。draftfalse

> Hugo 的渲染引擎符合 Markdown 的 CommonMark 规范。CommonMark组织提供了一个有用的实时测试工具，由参考实现提供支持。

## 配置站点
使用编辑器，打开项目根目录中的网站配置文件 （`hugo.toml`）。
```
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```
进行以下更改：

为您的生产站点设置`baseURL`。此值必须以协议开头，以斜杠结尾，如上所示。

设置`languageCode`为您的语言和地区。

为您的生产站点设置`title`。

启动 Hugo 的开发服务器以查看您的更改，记住包含草稿内容。
```
hugo server -D
```
> 大多数主题作者都提供配置指南和选项。有关详细信息，请务必访问主题的存储库或文档站点。
> New Dynamic是Ananke主题的作者，提供配置和使用的文档。他们还提供了一个示范点。

## 发布网站
在此步骤中，您将发布站点，但不会部署它。

当您发布站点时，Hugo 会在项目根目录中的目录中创建整个静态站点。这包括 HTML 文件和资产，例如图像、CSS 文件和 JavaScript 文件。public

发布网站时，通常不希望包含草稿、未来或过期内容。命令很简单。
```
hugo
```
若要了解如何部署站点，请参阅托管和部署部分。

## 寻求帮助
Hugo 的论坛是一个由用户和开发人员组成的活跃社区，他们回答问题、分享知识并提供示例。快速搜索超过 20,000 个主题通常可以回答您的问题。在提出第一个问题之前，请务必阅读有关请求帮助的信息。

## 其他资源
有关帮助您学习 Hugo 的其他资源，包括书籍和视频教程，请参阅外部学习资源页面。