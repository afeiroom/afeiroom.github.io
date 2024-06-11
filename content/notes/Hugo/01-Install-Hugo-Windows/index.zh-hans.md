---
title: Hugo 安装（Windows）
description: "Hugo 官网 Install Hugo on Windows 安装说明文档。"
# linkTitle:
date: 2024-04-19T01:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 1
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

# Hugo 安装（Windows）

	
## 参考内容

* [codingriver【Hugo 入门安装（Windows）】](https://blog.csdn.net/codingriver/article/details/107718847)
* [Hugo官网 Install Hugo on Windows](https://gohugo.io/installation/windows/)

## 安装Hugo说明
以下是 Hugo官网 Install Hugo on Windows 安装说明文档：

> Hugo v0.121.1 及更高版本至少需要 Windows 10 或 Windows Server 2016。

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
	*  [Git](https://git-scm.com/)
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

包管理器
Chocolatey 
Chocolatey 是适用于 Windows 的免费开源包管理器。要安装 Hugo 的扩展版本：

> choco install hugo-extended

Scoop 
Scoop 是适用于 Windows 的免费开源包管理器。要安装 Hugo 的扩展版本：

> scoop install hugo-extended

Winget 
Winget 是 Microsoft 官方的 Windows 免费开源包管理器。要安装 Hugo 的扩展版本：

> winget install Hugo.Hugo.Extended

安装方法三：从源代码构建
要从源代码构建 Hugo 的扩展版本，您必须：
1. 安装 Git
2. 安装 Go 版本 1.20 或更高版本
3. 安装 C 编译器，GCC 或 Clang
4. 按照 Go 文档中的说明更新环境变量 `PATH`
	> install 目录由 和 环境变量控制。如果设置，则二进制文件将安装到该目录。如果设置，则二进制文件将安装到列表中第一个目录的 bin 子目录中。否则，二进制文件将安装到默认 （ 或 ） 的 bin 子目录中。`GOPATHGOBINGOBINGOPATHGOPATHGOPATH$HOME/go%USERPROFILE%\go`
5. 然后构建并测试
	> CGO_ENABLED=1 go install -tags extended github.com/gohugoio/hugo@latest
hugo version


### 下载Hugo

下载：[下载Hugo](https://github.com/gohugoio/hugo/releases)

因为推荐安装扩展版，这里下载的是 `hugo_extended_0.125.1_windows-amd64.zip`

解压后有一个exe文件 `hugo.exe`

放在文件夹 `C:\hugo\bin\` 中

### 添加环境变量
然后将 `C:\hugo\bin\` 文件夹添加到环境变量中

右键 `此电脑` → `属性` → `系统>系统信息` → `高级系统设置` → `系统属性` → `环境变量` → `XXX的用户变量` → `Path` → `编辑` → `新建` → 填写：`C:\hugo\bin`

然后一路 `确定` 

### 查看 hugo 版本
hugo是命令行运行程序，需要开启 `CMD` `命令提示符` 程序。个人感觉 `Windows PowerShell` 不如 `CMD` 好用。

执行 `hugo version`
```
C:\Users\Super Typhoon>hugo version
hugo v0.125.1-68c5ad638c2072969e47262926b912e80fd71a77+extended windows/amd64 BuildDate=2024-04-18T08:21:19Z VendorInfo=gohugoio
```

出现版本号，配置完成。


## 创建站点项目

### 查看帮助 hugo help
```
C:\Users\Super Typhoon>hugo help
hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at https://gohugo.io/.

Usage:
  hugo [flags]
  hugo [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  config      Print the site configuration
  convert     Convert your content to different formats
  deploy      Deploy your site to a Cloud provider.
  env         Print Hugo version and environment info
  gen         A collection of several useful generators.
  help        Help about any command
  import      Import your site from others.
  list        Listing out various types of content
  mod         Various Hugo Modules helpers.
  new         Create new content for your site
  server      A high performance webserver
  version     Print Hugo version and environment info

Flags:
  -b, --baseURL string             hostname (and path) to the root, e.g. https://spf13.com/
  -D, --buildDrafts                include content marked as draft
  -E, --buildExpired               include expired content
  -F, --buildFuture                include content with publishdate in the future
      --cacheDir string            filesystem path to cache directory
      --cleanDestinationDir        remove files from destination not found in static directories
      --clock string               set the clock used by Hugo, e.g. --clock 2021-11-06T22:30:00.00+09:00
      --config string              config file (default is hugo.yaml|json|toml)
      --configDir string           config dir (default "config")
  -c, --contentDir string          filesystem path to content directory
      --debug                      debug output
  -d, --destination string         filesystem path to write files to
      --disableKinds strings       disable different kind of pages (home, RSS etc.)
      --enableGitInfo              add Git revision, date, author, and CODEOWNERS info to the pages
  -e, --environment string         build environment
      --forceSyncStatic            copy all files when static is changed.
      --gc                         enable to run some cleanup tasks (remove unused cache files) after the build
  -h, --help                       help for hugo
      --ignoreCache                ignores the cache directory
      --ignoreVendorPaths string   ignores any _vendor for module paths matching the given Glob pattern
  -l, --layoutDir string           filesystem path to layout directory
      --logLevel string            log level (debug|info|warn|error)
      --minify                     minify any supported output format (HTML, XML etc.)
      --noBuildLock                don't create .hugo_build.lock file
      --noChmod                    don't sync permission mode of files
      --noTimes                    don't sync modification time of files
      --panicOnWarning             panic on first WARNING log
      --poll string                set this to a poll interval, e.g --poll 700ms, to use a poll based approach to watch for file system changes
      --printI18nWarnings          print missing translations
      --printMemoryUsage           print memory usage to screen at intervals
      --printPathWarnings          print warnings on duplicate target paths etc.
      --printUnusedTemplates       print warnings on unused templates.
      --quiet                      build in quiet mode
      --renderSegments strings     named segments to render (configured in the segments config)
      --renderToMemory             render to memory (mostly useful when running the server)
  -s, --source string              filesystem path to read files relative from
      --templateMetrics            display metrics about template executions
      --templateMetricsHints       calculate some improvement hints when combined with --templateMetrics
  -t, --theme strings              themes to use (located in /themes/THEMENAME/)
      --themesDir string           filesystem path to themes directory
      --trace file                 write trace to file (not useful in general)
  -v, --verbose                    verbose output
  -w, --watch                      watch filesystem for changes and recreate as needed

Use "hugo [command] --help" for more information about a command.

C:\Users\Super Typhoon>
```

### 创建站点项目
假设要创建站点存放在 `C:\Hugo\Sites\` 目录中
在命令行切换到该目录下执行 `hugo new site afeiroom` 创建 `afeiroom` 站点项目（站点名称是自己起的名字）

```
C:\Users\Super Typhoon>cd c:\hugo		# 进入上面确定的 hugo 安装目录

c:\hugo>dir
 驱动器 C 中的卷是 TiPlus200G
 卷的序列号是 1288-03AB

 c:\hugo 的目录

2024/04/20  09:21    <DIR>          .
2024/04/20  09:21    <DIR>          bin
               0 个文件              0 字节
               2 个目录 78,998,056,960 可用字节

c:\hugo>md Sites				# 新建 Sites 文件夹

c:\hugo>cd Sites				# 进入 Sites 文件夹

c:\hugo\Sites>hugo new site afeiroom		# 创建 afeiroom 站点项目
Congratulations! Your new Hugo site was created in c:\hugo\Sites\afeiroom.

Just a few more steps...

1. Change the current directory to c:\hugo\Sites\afeiroom.
2. Create or install a theme:
   - Create a new theme with the command "hugo new theme <THEMENAME>"
   - Install a theme from https://themes.gohugo.io/
3. Edit hugo.toml, setting the "theme" property to the theme name.
4. Create new content with the command "hugo new content <SECTIONNAME>\<FILENAME>.<FORMAT>".
5. Start the embedded web server with the command "hugo server --buildDrafts".

See documentation at https://gohugo.io/.

c:\hugo\Sites>dir				# 查看此 Sites 文件夹
 驱动器 C 中的卷是 TiPlus200G
 卷的序列号是 1288-03AB

 c:\hugo\Sites 的目录

2024/04/20  12:19    <DIR>          .
2024/04/20  12:18    <DIR>          ..
2024/04/20  12:19    <DIR>          afeiroom	# hugo在 Sites 文件夹内新建 afeiroom 文件夹
               0 个文件              0 字节
               3 个目录 78,995,693,568 可用字节

c:\hugo\Sites>
```

### 查看新创建的站点项目结构

查看新创建的站点项目结构
```
c:\hugo\Sites>cd afeiroom				# 进入站点项目文件夹

c:\hugo\Sites\afeiroom>dir				# 查看站点项目文件夹文件结构
 驱动器 C 中的卷是 TiPlus200G
 卷的序列号是 1288-03AB

 c:\hugo\Sites\afeiroom 的目录

2024/04/20  12:19    <DIR>          .
2024/04/20  12:19    <DIR>          ..
2024/04/20  12:19    <DIR>          archetypes
2024/04/20  12:19    <DIR>          assets
2024/04/20  12:19    <DIR>          content
2024/04/20  12:19    <DIR>          data
2024/04/20  12:19                83 hugo.toml		# hugo 站点项目配置文件
2024/04/20  12:19    <DIR>          i18n
2024/04/20  12:19    <DIR>          layouts
2024/04/20  12:19    <DIR>          static
2024/04/20  12:19    <DIR>          themes
               1 个文件             83 字节
              10 个目录 78,777,831,424 可用字节

c:\hugo\Sites\afeiroom>
```

目前hugo v0.125.1创建项目的文件结构为：
```
├─archetypes
　　　├─default.md
├─assets
├─content
├─data
├─i18n
├─layouts
├─static
├─themes
└─hugo.toml						# hugo 站点项目配置文件
```

### 搭建站点
根据之前创建站点项目时的命令提示，一步一步操作：
```
Congratulations! Your new Hugo site was created in c:\hugo\Sites\afeiroom.

Just a few more steps...

1. Change the current directory to c:\hugo\Sites\afeiroom.
2. Create or install a theme:
   - Create a new theme with the command "hugo new theme <THEMENAME>"
   - Install a theme from https://themes.gohugo.io/
3. Edit hugo.toml, setting the "theme" property to the theme name.
4. Create new content with the command "hugo new content <SECTIONNAME>\<FILENAME>.<FORMAT>".
5. Start the embedded web server with the command "hugo server --buildDrafts".

See documentation at https://gohugo.io/.
```

用翻译软件翻译如下：
```
恭喜！您的新 Hugo 网站已在c:\hugo\Sites\afeiroom 中创建。

还有几个步骤……

1. 将当前目录更改为 c:\hugo\Sites\afeiroom。
2. 创建或安装一个主题：
   - 使用命令 hugo new theme <THEMENAME> 创建一个新主题
   - 从 https://themes.gohugo.io/ 安装一个主题
3. 编辑 hugo.toml，将 theme 属性设置为主题名称。
4. 使用命令 hugo new content <SECTIONNAME>\<FILENAME>.<FORMAT>创建新内容。
5. 使用命令 hugo server --buildDrafts 启动嵌入式Web服务器。

请参阅文档：https://gohugo.io/。
```


