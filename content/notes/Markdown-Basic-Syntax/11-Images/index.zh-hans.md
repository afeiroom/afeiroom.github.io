---
title: Markdown 图片语法
description: "要添加图像，请使用感叹号 ( ! ) ……"
# linkTitle:
date: 2024-04-11T11:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 11
nav_icon:
  vendor: bootstrap
  name: markdown
  color: HotPink
series:
  - Markdown 基本语法
categories:
  - 笔记
tags:
  - Markdown
images:
  - https://s2.loli.net/2024/06/09/OIoj32veAFQq4Zz.jpg?width=1920&height=1440
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

# Markdown 图片语法
要添加图像，请使用感叹号 (!), 然后在方括号增加替代文本，图片链接放在圆括号里，括号里的链接后可以增加一个可选的图片标题文本。

插入图片Markdown语法代码：`![图片alt](图片链接 "图片title")`。

对应的HTML代码：`<img src="图片链接" alt="图片alt" title="图片title">`
```

	![这是图片](/assets/img/philly-magic-garden.jpg "Magic Gardens")


```
渲染效果如下：

![这是图片](https://s2.loli.net/2024/06/09/4X1DiKf3kAw6gxq.png "Magic Gardens")

## 链接图片
给图片增加链接，请将图像的Markdown 括在方括号中，然后将链接添加在圆括号中。
```

	[![沙漠中的岩石图片](/assets/img/shiprock.jpg "Shiprock")](https://markdown.com.cn)
	
```
渲染效果如下：

[![沙漠中的岩石图片](https://s2.loli.net/2024/06/09/usOmqedgJwMNXvt.png "Shiprock")](https://markdown.com.cn)
