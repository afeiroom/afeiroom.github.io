---
title: Markdown 使用 Emoji 表情
description: "有两种方法可以将表情符号添加到Markdown文件中。"
# linkTitle:
date: 2024-04-12T10:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 10
nav_icon:
  vendor: bootstrap
  name: pencil-square
  color: Blue
series:
  - Markdown 扩展语法
categories:
  - 笔记
tags:
  - Markdown
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

# Markdown 使用 Emoji 表情
有两种方法可以将表情符号添加到Markdown文件中：将表情符号复制并粘贴到Markdown格式的文本中，或者键入*emoji shortcodes*。

## 复制和粘贴表情符号
在大多数情况下，您可以简单地从[Emojipedia](https://emojipedia.org/) 等来源复制表情符号并将其粘贴到文档中。许多Markdown应用程序会自动以Markdown格式的文本显示表情符号。从Markdown应用程序导出的HTML和PDF文件应显示表情符号。

**Tip:** 如果您使用的是静态网站生成器，请确保将HTML页面编码为UTF-8。
## 使用表情符号简码
一些Markdown应用程序允许您通过键入表情符号短代码来插入表情符号。这些以冒号开头和结尾，并包含表情符号的名称。

~~~

	去露营了！ :tent: 很快回来。

	真好笑！ :joy:


~~~

呈现的输出如下所示：

去露营了！⛺很快回来。

真好笑！😂

**注意**：您可以使用此[表情符号简码列表](https://gist.github.com/rxaviers/7360908)，但请记住，表情符号简码因应用程序而异[^1]。有关更多信息，请参阅Markdown应用程序的文档。

[^1]: Mkdocs网站不支持此功能。
