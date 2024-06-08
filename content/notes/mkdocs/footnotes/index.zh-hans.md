---
title: 脚注扩展
updated: 2024-04-13 11:10:45Z
created: 2024-04-13 02:29:38Z
latitude: 28.68289200
longitude: 115.85819800
altitude: 0.0000

description: "脚注是在不中断文档流程的情况下向特定单词、短语或句子添加补充或附加信息的好方法。"
# linkTitle:
date: 2024-04-13T20:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 5
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
  - https://s2.loli.net/2024/05/11/gDsmGfS4HeJNPZ8.jpg?width=1920&height=1440
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

# 脚注扩展

	
脚注是在不中断文档流程的情况下向特定单词、短语或句子添加补充或附加信息的好方法。MkDocs 的材质提供了定义、引用和呈现脚注的功能。

## 配置
此配置增加了定义内联脚注的功能，这些脚注随后呈现在文档的所有 Markdown 内容下方。将以下行添加到：mkdocs.yml
```

markdown_extensions:
  - footnotes
  
```
