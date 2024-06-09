---
title: Markdown 定义列表
description: "一些Markdown处理器允许您创建术语及其对应定义的定义列表。"
# linkTitle:
date: 2024-04-12T07:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 7
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

# Markdown 定义列表
一些Markdown处理器允许您创建术语及其对应定义的定义列表。要创建定义列表，请在第一行上键入术语。在下一行，键入一个冒号，后跟一个空格和定义。
```

	First Term
	: This is the definition of the first term.

	Second Term
	: This is one definition of the second term.
	: This is another definition of the second term.


```
HTML看起来像这样：
```

  <dl>
    <dt>First Term</dt>
    <dd>This is the definition of the first term.</dd>
    <dt>Second Term</dt>
    <dd>This is one definition of the second term. </dd>
    <dd>This is another definition of the second term.</dd>
  </dl>


```
呈现的输出如下所示[^1]：

<dl>
  <dt>First Term</dt>
  <dd>This is the definition of the first term.</dd>
  <dt>Second Term</dt>
  <dd>This is one definition of the second term. </dd>
  <dd>This is another definition of the second term.</dd>
</dl>

[^1]: Mkdocs网站不支持此功能，以上示例是由HTML语法呈现。