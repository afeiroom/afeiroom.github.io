---
title: Markdown 上标
uupdescription: "某些 Markdown 处理器允许您使用上标。"
# linkTitle:
date: 2024-04-12T14:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 14
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

# Markdown 上标
这并不常见，但某些 Markdown 处理器允许您使用上标将一个或多个字符放置在略高于正常类型行的位置。要创建上标，请在字符前后使用一个插入符号 （`^`）。[^1]
[^1]: Mkdocs网站不支持此功能，渲染示例通过HTML标记实现。
```

	X^2^
	
```
渲染的输出如下所示：

X<sup>2</sup>

或者，如果 Markdown 应用程序支持 HTML，则可以使用 HTML 标记。sup
```

	X<sup>2</sup>
	
```

