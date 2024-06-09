---
title: Markdown 自动网址链接
description: "许多Markdown处理器会自动将URL转换为链接。"
# linkTitle:
date: 2024-04-12T11:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 11
nav_icon:
  vendor: bootstrap
  name: pencil-square
  color: HotPink
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

# Markdown 自动网址链接
许多Markdown处理器会自动将URL转换为链接。这意味着如果您输入http://www.example.com，即使您未使用方括号，您的Markdown处理器也会自动将其转换为链接。
```

	http://www.example.com


```
呈现的输出如下所示：

http://www.example.com


## 禁用自动URL链接
如果您不希望自动链接URL，则可以通过将URL表示为带反引号的代码来删除该链接。
```

	`http://www.example.com`


```
呈现的输出如下所示：

`http://www.example.com`
