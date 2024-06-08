---
title: 格式扩展
description: "MkDocs 通过扩展支持多个 HTML 元素。"
# linkTitle:
date: 2024-04-13T17:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 2
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
  - https://s2.loli.net/2024/05/11/tAGhYaXn6zSvQdN.jpg?width=1920&height=1440
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

# 格式扩展

	
MkDocs 的材质支持多个 HTML 元素，这些元素可用于突出显示文档的各个部分或应用特定格式。此外，还支持批注者标记，增加了显示文档建议更改的功能。

## 配置
此配置支持键盘键、跟踪文档中的更改、定义下标和上标以及突出显示文本。将以下行添加到：mkdocs.yml

```

markdown_extensions:
  - pymdownx.critic
  - pymdownx.caret
  - pymdownx.keys
  - pymdownx.mark
  - pymdownx.tilde
  
 ```
