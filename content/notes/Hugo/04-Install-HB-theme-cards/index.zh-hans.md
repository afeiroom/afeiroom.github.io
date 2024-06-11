---
title: 在 Linux 上安装HB（Hugo Bootstrap）
description: "历经坎坷，最终把 HB theme-cards 主题从头开始安装，终于成功了。"
# linkTitle:
date: 2024-04-28T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 4
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
  - HB theme-cards
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

# 在 Linux 上安装HB（Hugo Bootstrap）

	
HB（Hugo Bootstrap）是一个模块化的框架，其构建于 Hugo 和 Bootstrap 之上。 HB 不是一个主题，而是用来建立一个主题的。

> 1. 此贴中，安装 HB 没成功；
> 2. 此贴中，安装 HB Start Theme 主题没成功；
> 3. 最终，HB theme-cards 主题从头开始安装，**终于成功了**。

## 先决条件

HB 是一个功能丰富的框架，但同时也具有着一定的复杂性。本文将详细列出 HB 的环境要求，以便你可以正常地开发和使用 HB 模块和主题。

### 必要配置

TOML 模式配置

hugo.toml
~~~
[build]
  writeStats = true
~~~

YAML 模式配置

hugo.yaml
```
build:
  writeStats: true
```

JSON 模式配置

hugo.json
```
{
   "build": {
      "writeStats": true
   }
}
```

`build.writeStats`
用于收集站点所使用到的 classes、ids 和 tags，以供 PurgeCSS 清除未使用的 CSS。

### 构建工具
推荐尽可能地使用以下构建工具的最新版本。

#### Go
HB 是一个模块化的框架，需要安装 Go 语言以下载和更新 Hugo 模块。

`Arch Linux 安装 Go`

#### Hugo

HB 使用 Hugo Pipes 来编译 SCSS，因此需要扩展版（extended）的 Hugo。

`通过 Go 安装 Hugo`

#### Git
版本控制系统，可通过下载页面获得。

`Arch Linux 安装 Git`

#### Node.js

> 要求 Node.js 16 或后续版本。

`Arch Linux 安装 Node.js`

HB 依赖以下 Node.js 包。

| 名称         | 描述                                               |
| :----------- | :------------------------------------------------- |
| PostCSS      | CLI	用于转变样式。                                 |
| RTLCSS       | 将 LTR CSS 转换为 RTL，如果你没有 RTL 网站则可选。 |
| Autoprefixer | 解析 CSS 并在 Can I Use 规则中添加对应的前缀。     |
| PurgeCSS     | 移除未使用的 CSS。                                 |

NPM 已被包含于 Node.js 安装中，你可以选择局部或全局地安装这些包。

* 局部安装
```
npm i -D postcss-cli @fullhuman/postcss-purgecss autoprefixer rtlcss
```

局部安装将依赖写入 `package.json`，以便部署时通过 `npm i` 安装这些包，而无需记住这些繁杂的包名。

* 全局安装
```
sudo npm i -g postcss-cli @fullhuman/postcss-purgecss autoprefixer rtlcss
```

该命令只需执行一次，后续的 HB 站点无需再次执行此命令。

两者都是有效的，HB 会优先局部查找需要的包。


### Hugo Server 生产模式的必要参数
若需要在生产模式下使用 Hugo Server，需要指定 `--disableFastRender` 和 `--renderToDisk`，否则 PurgeCSS 和 PostCSS 会出现意想不到的问题。
```
hugo server \
  --disableFastRender \
  --renderToDisk \
  -e production \
  -b http://localhost:1314 \
  -p 1314
```
### 请勿于语言范围配置中修改 `hb` 和 `hugopress` 参数
HB 依赖于模块间配置的深度合并，然而语言范围的参数将会覆盖覆盖模块的配置，而非深度合并，这将导致各种意想不到的问题。比如以下的配置示例是**不允许**的。

TOML 模式配置
hugo.toml
```
[language]
  [language.en]
    [language.en.params]
      [language.en.params.hb]
        foo = 'bar'
      [language.en.params.hugopress]
        foo = 'bar'
  [language.zh-hans]
    [language.zh-hans.params]
      [language.zh-hans.params.hb]
        foo = 'bar'
      [language.zh-hans.params.hugopress]
        foo = 'bar'
```

YAML 模式配置
hugo.yaml
```
language:
  en:
    params:
      hb:
        foo: bar
      hugopress:
        foo: bar
  zh-hans:
    params:
      hb:
        foo: bar
      hugopress:
        foo: bar
```

JSON 模式配置
hugo.json
```
{
   "language": {
      "en": {
         "params": {
            "hb": {
               "foo": "bar"
            },
            "hugopress": {
               "foo": "bar"
            }
         }
      },
      "zh-hans": {
         "params": {
            "hb": {
               "foo": "bar"
            },
            "hugopress": {
               "foo": "bar"
            }
         }
      }
   }
}
```

### 请禁用 Cloudflare Rocket Loader
Cloudflare Rocket Loader 缺少了 `DOMContentLoaded` 事件，会导致很多模块失效，即便我们为此提供了一个补丁，但得不偿失，禁用该功能是目前最佳选择。

## 安装

我们提供了一个入门主题模板，以便你快速地创建一个 HB 站点。

一分钟安装 HB 主题。

```
[root@192 ~]# mkdir tmp
[root@192 ~]# cd tmp
[root@192 tmp]# git clone --depth 1 https://github.com/hbstack/theme blog
正克隆到 'blog'...
fatal: unable to access 'https://github.com/hbstack/theme/': Empty reply from server

### Git取消代理
### 当出现以上报错的时候，你第一步可以采取的方法就是通过以下Git命令取消proxy代理，然后再回到你前面要执行的步骤
### 解决不能访问的问题：通过git取消代理
### git config --global --unset http.proxy
### git config --global --unset https.proxy

[root@192 tmp]# git config --global --unset http.proxy
[root@192 tmp]# git config --global --unset https.proxy

[root@192 tmp]# git clone --depth 1 https://github.com/hbstack/theme blog
正克隆到 'blog'...
remote: Enumerating objects: 213, done.
remote: Counting objects: 100% (213/213), done.
remote: Compressing objects: 100% (158/158), done.
remote: Total 213 (delta 16), reused 188 (delta 14), pack-reused 0
接收对象中: 100% (213/213), 61.08 MiB | 13.68 MiB/s, done.
处理 delta 中: 100% (16/16), done.

[root@192 tmp]# ls
blog
[root@192 tmp]# cd blog

[root@192 blog]# npm ci

added 110 packages in 2s

33 packages are looking for funding
  run `npm fund` for details

[root@192 blog]# npm run dev

> dev
> hugo server --gc --enableGitInfo -D

hugo: downloading modules …
^C
[root@192 blog]#
```


```
[root@localhost blog]# npm run dev

> dev
> hugo server --gc --enableGitInfo -D

hugo: downloading modules …
hugo: collected modules in 24089 ms
Watching for changes in /root/tmp/blog/{archetypes,assets,content,layouts,package.json}
Watching for config changes in /root/tmp/blog/config/_default, /root/tmp/blog/config/development, /root/tmp/blog/go.mod
Start building sites …
hugo v0.125.4-cc3574ef4f41fccbe88d9443ed066eb10867ada2+extended linux/amd64 BuildDate=2024-04-25T13:27:26Z VendorInfo=gohugoio

ERROR Failed to read Git log: Unknown option: -C
usage: git [--version] [--help] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

```

### Go 和 Hugo 代理服务器
Go 官方的模块代理服务器被 GFW 墙了，没有 VPN 的情况下，于国内是无法正常使用的。不过可以通过设置代理服务器解决，本文将列出一些可用的 Go 代理服务器。而这也同样适用于 Hugo 模块。

* 代理服务器

| 代理服务器          | URL                                 |
| :------------------ | :---------------------------------- |
| GOPROXY.CN (七牛云) | https://goproxy.cn/                 |
| GOPROXY.IO          | https://goproxy.io/                 |
| 阿里云              | https://mirrors.aliyun.com/goproxy/ |
| 腾讯云              | https://mirrors.tencent.com/go/     |

设置 Go 模块代理服务器
```
export GOPROXY=https://goproxy.cn/,direct
```
或者
```
go env -w GOPROXY=https://goproxy.cn/,direct
```
设置 Hugo 模块代理服务器
与 Go 不同，Hugo 使用 `HUGO_MODULE_PROXY` 环境变量而非 `GOPROXY`。
```
export HUGO_MODULE_PROXY=https://goproxy.cn/,direct
```
也可以于配置中设置。

YAML 模式配置

hugo.yaml
```
module:
  proxy: https://goproxy.cn
```
TOML 模式配置
hugo.toml
```
[module]
  proxy = 'https://goproxy.cn'
```
JSON 模式配置
hugo.json
```
{
   "module": {
      "proxy": "https://goproxy.cn"
   }
}
```


```
[root@localhost blog]# export GOPROXY=https://goproxy.cn/,direct
[root@localhost blog]# export HUGO_MODULE_PROXY=https://goproxy.cn/,direct
[root@localhost blog]# npm run dev

> dev
> hugo server --gc --enableGitInfo -D

hugo: downloading modules …
hugo: collected modules in 24089 ms
Watching for changes in /root/tmp/blog/{archetypes,assets,content,layouts,package.json}
Watching for config changes in /root/tmp/blog/config/_default, /root/tmp/blog/config/development, /root/tmp/blog/go.mod
Start building sites …
hugo v0.125.4-cc3574ef4f41fccbe88d9443ed066eb10867ada2+extended linux/amd64 BuildDate=2024-04-25T13:27:26Z VendorInfo=gohugoio

ERROR Failed to read Git log: Unknown option: -C
usage: git [--version] [--help] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
WARN  image not found: /en/docs/installation/linux/ubuntu/feature.png?height=360px
WARN  image not found: /en/blog/2022/02/example-post-with-an-featured-image/featured.jpeg?height=360px
ERROR POSTCSS: failed to transform "css/hb.css" (text/css). Check your PostCSS installation; install with "npm install postcss-cli". See https://gohugo.io/hugo-pipes/postcss/: binary with name "npx" not found
Built in 100330 ms
Error: error building site: POSTCSS: failed to transform "css/hb.css" (text/css). Check your PostCSS installation; install with "npm install postcss-cli". See https://gohugo.io/hugo-pipes/postcss/: binary with name "npx" not found
[root@localhost blog]# npm install postcss-cli

up to date in 1s

33 packages are looking for funding
  run `npm fund` for details
[root@localhost blog]# npm fund

```

设置代理后还是报错，两个错误：

```
ERROR Failed to read Git log: Unknown option: -C

Error: error building site: POSTCSS: failed to transform "css/hb.css" (text/css). Check your PostCSS installation; install with "npm install postcss-cli". See https://gohugo.io/hugo-pipes/postcss/: binary with name "npx" not found
```

其中下面解决错误：
```
[root@localhost blog]# npm install postcss-cli

up to date in 1s

33 packages are looking for funding
  run `npm fund` for details
```


```
[root@localhost blog]# npm install npx

added 1 package in 5s

34 packages are looking for funding
  run `npm fund` for details
```

再次运行还是报错：
```
[root@localhost blog]# npm run dev

> dev
> hugo server --gc --enableGitInfo -D

Watching for changes in /root/tmp/blog/{archetypes,assets,content,layouts,package.json}
Watching for config changes in /root/tmp/blog/config/_default, /root/tmp/blog/config/development, /root/tmp/blog/go.mod
Start building sites …
hugo v0.125.4-cc3574ef4f41fccbe88d9443ed066eb10867ada2+extended linux/amd64 BuildDate=2024-04-25T13:27:26Z VendorInfo=gohugoio

ERROR Failed to read Git log: Unknown option: -C
usage: git [--version] [--help] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
WARN  image not found: /en/docs/installation/linux/ubuntu/feature.png?height=360px
WARN  image not found: /en/blog/2022/02/example-post-with-an-featured-image/featured.jpeg?height=360px
Built in 4134 ms
Error: error building site: logged 1 error(s)

```

====不知道如何解决，暂时鸽了====


Hugo 服务器在第一次运行时需要很长的时间以下载模块和处理大量图片，你需要删除无用的图片和提交 resources/images 文件夹以提高构建性能。



克隆仓库
git clone --depth 1 https://github.com/hbstack/theme blog
SH
cd blog
SH
其中的 blog 是本地目录名称，请随意修改。

模块路径
首先修改位于 go.mod 的模块路径，将其中的 module github.com/hbstack/theme 替换为你的，如：module github.com/user/repo。

sed -i -e 's/module\ github.com\/hbstack\/theme/module\ github.com\/user\/repo/' go.mod
SH
推送到远程仓库
提交改动
git add .

git commit --amend
SH
修改提交信息保存即可，如：First commit。

修改远程仓库
git remote set-url origin https://github.com/user/repo
SH
推送
git push origin main
SH
Hugo 模块代理（可选）
如果你在中国大陆没有 VPN，Hugo 模块的下载可能会失败。另请参阅Go 和 Hugo 代理服务器。

安装构建工具
npm ci
SH
请注意 Go 和 Node.js 是必要条件，详情请参阅构建工具。

启动 Hugo 服务器
于开发模式下预览
npm run dev
SH
于生产模式下预览
npm run prod
SH
下一步


## 安装 HB Start Theme 主题

### 克隆仓库
```
git clone --depth 1 https://github.com/hbstack/theme-start
```
### 复制示例站点
```
cp -r theme-start/exampleSite ./start-page
```

```
### cp [选项] 源文件 目标文件

### 选项说明：
###   -r 或 --recursive：用于复制目录及其所有的子目录和文件，如果要复制目录，需要使用该选项。
```
### 更改工作目录
```
cd start-page
```
### 重新初始化站点
```
rm go.mod go.sum config/_default/module.yaml
hugo mod init [MODULE_PATH]
```
这 `[MODULE_PATH]` 是您网站的标识符，通常是存储库 URL，即 `example.com/user/repo`。

```
[root@localhost tmp]# git clone --depth 1 https://github.com/hbstack/theme-start
正克隆到 'theme-start'...
remote: Enumerating objects: 129, done.
remote: Counting objects: 100% (129/129), done.
remote: Compressing objects: 100% (102/102), done.
remote: Total 129 (delta 13), reused 92 (delta 9), pack-reused 0
接收对象中: 100% (129/129), 2.22 MiB | 953.00 KiB/s, done.
处理 delta 中: 100% (13/13), done.
[root@localhost tmp]# ls
blog  theme-start
[root@localhost tmp]# cp -r theme-start/exampleSite ./start-page
[root@localhost tmp]# ls
blog  start-page  theme-start
[root@localhost tmp]# cd start-page
[root@localhost start-page]# ls
assets  config  content  data  go.mod  go.sum  layouts  package.json  package-lock.json
[root@localhost start-page]# rm go.mod go.sum config/_default/module.yaml
rm：是否删除普通文件 "go.mod"？y
rm：是否删除普通文件 "go.sum"？y
rm：是否删除普通文件 "config/_default/module.yaml"？y
[root@localhost start-page]# hugo mod init afeiroom.gitee.io
```

config/_default/module.yaml

sed -i '1s/.*/module afeiroom.gitee.io/' go.mod


### 导入主题和搜索引擎

====不知道如何解决，也鸽了====

# HB theme-cards 主题从头开始安装

  　　————2024.4.29

从头开始使用 HB 卡主题构建快速、响应式和模块化静态网站。
## 参考链接

* [HB 从头开始安装](https://theme-cards.hbstack.dev/zh-hans/docs/install-from-scratch/)

## 环境要求

* 有关安装说明，请参阅相关文档：
	* [Git](https://git-scm.com/)
	* [Go](https://go.dev/) 
	* [Hugo 扩展版](https://gohugo.io/installation)
	* [Node.js 16 或更高版本](http://nodejs.cn/download/)

了解更多关于[先决条件](https://zh-hans.hbstack.dev/docs/getting-started/prerequisites/)的内容。

## 克隆仓库
```
git clone --depth 1 https://github.com/hbstack/theme-cards
```
具体执行命令：
```
[root@localhost tmp]# mkdir blog
[root@localhost tmp]# cd blog/
[root@localhost blog]# ls
[root@localhost blog]# git clone --depth 1 https://github.com/hbstack/theme-cards
正克隆到 'theme-cards'...
remote: Enumerating objects: 193, done.
remote: Counting objects: 100% (193/193), done.
remote: Compressing objects: 100% (130/130), done.
remote: Total 193 (delta 12), reused 157 (delta 8), pack-reused 0
接收对象中: 100% (193/193), 1.70 MiB | 1.17 MiB/s, done.
处理 delta 中: 100% (12/12), done.
```

## 复制示例站点
```
cp -r theme-cards/exampleSite mysite
```

具体执行命令：
```
[root@localhost blog]# cp -r theme-cards/exampleSite mysite
[root@localhost blog]# cd mysite
```
## 更改工作目录
```
cd mysite
```

具体执行命令：
```
[root@localhost blog]# cd mysite
```
## 调整 `go.mod`
> 本文利用 sed 命令进行文件编辑，请随意使用你喜欢的编辑器打开和修改 go.mod。
### 替换模块路径
模块路径是站点的标识，其一般为仓库 URL，这里以 `github.com/user/repo` 为例，则需要将 `module github.com/hbstack/theme-cards/exampleSite` 替换为 `module github.com/user/repo`。
```
sed -i '1s/.*/module github.com\/user\/repo/' go.mod
```

具体执行命令：
```
[root@localhost mysite]# sed -i '1s/.*/module afeiroom.gitee.io/' go.mod
```

## 删除 replace 指令
为了成功地构建站点，需要删除该内部使用的 `replace` 指令行：`replace github.com/hbstack/theme-cards => ../`。
```
sed -i '/^replace/d' go.mod
```

具体执行命令：
```
[root@localhost mysite]# sed -i '/^replace/d' go.mod
```
## 安装依赖
```
npm ci
```

具体执行命令：
```
[root@localhost mysite]# npm ci
npm WARN deprecated @hapi/formula@2.0.0: Moved to 'npm install @sideway/formula'
npm WARN deprecated @hapi/address@4.1.0: Moved to 'npm install @sideway/address'
npm WARN deprecated @hapi/joi@17.1.1: Switch to 'npm install joi'

added 224 packages in 12s

46 packages are looking for funding
  run `npm fund` for details
```
## Hugo 模块代理（可选）
当你的所在地区（比如国内）无法访问默认的代理时，则需要设置Hugo 模块代理。

### Go 和 Hugo 代理服务器
Go 官方的模块代理服务器被 GFW 墙了，没有 VPN 的情况下，于国内是无法正常使用的。不过可以通过设置代理服务器解决，本文将列出一些可用的 Go 代理服务器。而这也同样适用于 Hugo 模块。

* 代理服务器

| 代理服务器          | URL                                 |
| :------------------ | :---------------------------------- |
| GOPROXY.CN (七牛云) | https://goproxy.cn/                 |
| GOPROXY.IO          | https://goproxy.io/                 |
| 阿里云              | https://mirrors.aliyun.com/goproxy/ |
| 腾讯云              | https://mirrors.tencent.com/go/     |

设置 Go 模块代理服务器
```
export GOPROXY=https://goproxy.cn/,direct
```
或者
```
go env -w GOPROXY=https://goproxy.cn/,direct
```
设置 Hugo 模块代理服务器
与 Go 不同，Hugo 使用 `HUGO_MODULE_PROXY` 环境变量而非 `GOPROXY`。
```
export HUGO_MODULE_PROXY=https://goproxy.cn/,direct
```
也可以于配置中设置。

YAML 模式配置

hugo.yaml
```
module:
  proxy: https://goproxy.cn
```
TOML 模式配置
hugo.toml
```
[module]
  proxy = 'https://goproxy.cn'
```
JSON 模式配置
hugo.json
```
{
   "module": {
      "proxy": "https://goproxy.cn"
   }
}
```

具体执行命令：
```
[root@localhost mysite]# export GOPROXY=https://goproxy.cn/,direct
[root@localhost mysite]# export HUGO_MODULE_PROXY=https://goproxy.cn/,direct
```


## 本地预览
```
npm run dev
```

具体执行命令：
```
[root@localhost mysite]# npm run dev

> dev
> hugo server --gc -D

hugo: downloading modules …
hugo: collected modules in 5297 ms
Watching for changes in /root/tmp/blog/mysite/{archetypes,assets,content,layouts,package.json}
Watching for config changes in /root/tmp/blog/mysite/config/_default, /root/tmp/blog/mysite/config/development, /root/tmp/blog/mysite/go.mod
Start building sites …
hugo v0.125.4-cc3574ef4f41fccbe88d9443ed066eb10867ada2+extended linux/amd64 BuildDate=2024-04-25T13:27:26Z VendorInfo=gohugoio


                   | EN  | ZH-HANS
-------------------+-----+----------
  Pages            | 144 |     142
  Paginator pages  |   0 |       0
  Non-page files   |   0 |       0
  Static files     |   0 |       0
  Processed images |   9 |       0
  Aliases          |  67 |      66
  Cleaned          |   0 |       0

Built in 3998 ms
Environment: "development"
Serving pages from disk
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop

```

