---
title: Markdown 分隔线语法
description: "要创建分隔线，请在单独一行上使用三个或多个星号 ( *** )、破折号 ( --- ) 或下划线 ( ___ ) ，并且不能包含其他内容。"
# linkTitle:
date: 2024-04-11T09:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 9
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
  - https://s2.loli.net/2024/06/09/lGqHxuWINC8Te6J.jpg?width=1920&height=1440
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

# Markdown 分隔线语法

要创建分隔线，请在单独一行上使用三个或多个星号 (`***`)、破折号 (`---`) 或下划线 (`___`) ，并且不能包含其他内容。
```

***

---

__________
	
```

以上三个分隔线的渲染效果看起来都一样：

---

## 分隔线（Horizontal Rule）用法最佳实践

为了兼容性，请在分隔线的前后均添加空白行。

| ✅  Do this                                                                                      | ❌  Don't do this                                                                 |
| :---------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------- |
| `Try to put a blank line before...`<br /><br />`---`<br /><br />`and after a horizontal rule.	` | `Without blank lines, this would be a heading.`<br />`---`<br />`Don't do this!` |


