---
title: Markdown 代码语法
description: "要将单词或短语表示为代码，请将其包裹在反引号 ( ` ) 中"
# linkTitle:
date: 2024-04-11T08:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 8
nav_icon:
  vendor: bootstrap
  name: pencil-square
  color: Blue
series:
  - Markdown 基本语法
categories:
  - 笔记
tags:
  - Markdown
images:
  - https://s2.loli.net/2024/06/09/r3sYx6mWdSkXaCM.jpg?width=1920&height=1440
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

# Markdown 代码语法

要将单词或短语表示为代码，请将其包裹在反引号 (`` ` ``) 中。

| Markdown语法                            | HTML                                             | 预览效果                            |
| :-------------------------------------- | :----------------------------------------------- | :---------------------------------- |
| ``At the command prompt, type `nano`.`` | `At the command prompt, type <code>nano</code>.` | At the command prompt, type `nano`. |

## 转义反引号

如果你要表示为代码的单词或短语中包含一个或多个反引号，则可以通过将单词或短语包裹在双反引号(`` ` ` ``)中。

| Markdown语法                          | HTML                                               | 预览效果                              |
| :------------------------------------ | :------------------------------------------------- | :------------------------------------ |
| ``Use `code` in your Markdown file.`` | ``<code>Use `code` in your Markdown file.</code>`` | ``Use `code` in your Markdown file.`` |

*注：Markdown语法中的代码外面还有双反引号(`` ` ` ``)，我写不上。*

## 代码块

要创建代码块，请将代码块的每一行缩进至少四个空格或一个制表符。
```

    <html>
        <head>
        </head>
    </html>


```
渲染效果如下：



		<html>
			<head>
			</head>
		</html>

**Note**：要创建不用缩进的代码块，请使用 [围栏式代码块（fenced code blocks）]().

