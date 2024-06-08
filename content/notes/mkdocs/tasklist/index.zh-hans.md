---
title: 任务列表扩展
description: "MkDocs 通过扩展支持多种类型的列表。"
# linkTitle:
date: 2024-04-13T18:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 3
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
  - https://s2.loli.net/2024/05/11/O14pCArmhSMXvYN.jpg?width=1920&height=1440
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

# 任务列表扩展

  　　————2024.4.13
	
Material for MkDocs 支持多种类型的列表，以满足不同的用例，包括通过标准 Markdown 支持的无序列表和有序列表，以及通过扩展支持的定义列表和任务列表。

## 配置
此配置允许使用定义列表和任务列表，它们都不是标准 Markdown 语法的一部分。将以下行添加到：mkdocs.yml
```

markdown_extensions:
  - def_list
  - pymdownx.tasklist:
      custom_checkbox: true
	  
```
