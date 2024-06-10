---
title: Markdown 列表语法
description: "可以将多个条目组织成有序或无序列表。"
# linkTitle:
date: 2024-04-11T07:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 7
nav_icon:
  vendor: bootstrap
  name: pencil-square
  color: RoyalBlue
series:
  - Markdown 基本语法
categories:
  - 笔记
tags:
  - Markdown
images:
  - https://s2.loli.net/2024/06/09/jGn5AWeySBo9zM2.jpg?width=1920&height=1440
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

# Markdown 列表语法

可以将多个条目组织成有序或无序列表。

## 有序列表

要创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。数字不必按数学顺序排列，但是列表应当以数字 1 起始。

| Markdown语法                                                                                                                             | HTML                                                                                                                                                                                                                           | 预览效果                                                                                                           |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| `1. First item`<br />`2. Second item`<br />`3. Third item`<br />`4. Fourth item`                                                         | `<ol>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item</li>`<br />`<li>Fourth item</li>`<br />`</ol>`                                                                                              | 1.First item<br />2.Second item<br />3.Third item<br />4.Fourth item                                               |
| `1. First item`<br />`1. Second item`<br />`1. Third item`<br />`1. Fourth item`                                                         | `<ol>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item</li>`<br />`<li>Fourth item</li>`<br />`</ol>`                                                                                              | 1.First item<br />2.Second item<br />3.Third item<br />4.Fourth item                                               |
| `1. First item`<br />`8. Second item`<br />`3. Third item`<br />`5. Fourth item`                                                         | `<ol>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item</li>`<br />`<li>Fourth item</li>`<br />`</ol>`                                                                                              | 1.First item<br />2.Second item<br />3.Third item<br />4.Fourth item                                               |
| `1. First item`<br />`2. Second item`<br />`3. Third item`<br />`　　1. Indented item`<br />`　　2. Indented item`<br />`4. Fourth item` | `<ol>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item`<br />`<ol>`<br />`<li>Indented item</li>`<br />`<li>Indented item</li>`<br />`</ol>`<br />`</li>`<br />`<li>Fourth item</li>`<br />`</ol>` | 1.First item<br />2.Second item<br />3.Third item<br />　1.Indented item<br />　2.Indented item<br />4.Fourth item |

### 有序列表最佳实践

CommonMark 和其他一些轻量级标记语言允许您使用括号 （`)`） 作为分隔符（例如，`1) First item`），但并非所有 Markdown 应用程序都支持此功能，因此从兼容性的角度来看，它不是一个好的选择。为了兼容性，仅使用英文句点。

| ✅  Do this                            | ❌  Don't do this                      |
| :------------------------------------ | :------------------------------------ |
| `1. First item`<br />`2. Second item` | `1) First item`<br />`2) Second item` |
## 无序列表
要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (\*) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。

| Markdown语法                                                                                                                       | HTML                                                                                                                                                                                                                           | 预览效果                                                                                                           |
| :--------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| `- First item`<br />`- Second item`<br />`- Third item`<br />`- Fourth item`                                                       | `<ul>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item</li>`<br />`<li>Fourth item</li>`<br />`</ul>`                                                                                              | ● First item<br />● Second item<br />● Third item<br />● Fourth item                                               |
| `* First item`<br />`* Second item`<br />`* Third item`<br />`* Fourth item`                                                       | `<ul>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item</li>`<br />`<li>Fourth item</li>`<br />`</ul>`                                                                                              | ● First item<br />● Second item<br />● Third item<br />● Fourth item                                               |
| `+ First item`<br />`+ Second item`<br />`+ Third item`<br />`+ Fourth item`                                                       | `<ul>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item</li>`<br />`<li>Fourth item</li>`<br />`</ul>`                                                                                              | ● First item<br />● Second item<br />● Third item<br />● Fourth item                                               |
| `- First item`<br />`- Second item`<br />`- Third item`<br />`　　- Indented item`<br />`　　- Indented item`<br />`- Fourth item` | `<ul>`<br />`<li>First item</li>`<br />`<li>Second item</li>`<br />`<li>Third item`<br />`<ul>`<br />`<li>Indented item</li>`<br />`<li>Indented item</li>`<br />`</ul>`<br />`</li>`<br />`<li>Fourth item</li>`<br />`</ul>` | ● First item<br />● Second item<br />● Third item<br />　○ Indented item<br />　○ Indented item<br />● Fourth item |

### 无序列表最佳实践
Markdown 应用程序在如何处理同一列表中的不同分隔符方面不一致。为了兼容性，不要在同一列表中混合和匹配分隔符——选择一个并坚持使用。

| ✅  Do this                                                                   | ❌  Don't do this                                                             |
| :--------------------------------------------------------------------------- | :--------------------------------------------------------------------------- |
| `- First item`<br />`- Second item`<br />`- Third item`<br />`- Fourth item` | `+ First item`<br />`* Second item`<br />`- Third item`<br />`+ Fourth item` |

## 在列表中嵌套其他元素

要在保留列表连续性的同时在列表中添加另一种元素，请将该元素缩进四个空格或一个制表符，如下例所示：

### 段落
```

	* 　This is the first list item.
	* 　Here's the second list item.
	　　I need to add another paragraph below the second list item.
	* 　And here's the third list item.


```
渲染效果如下：

*	This is the first list item.
* 	Here's the second list item.
		I need to add another paragraph below the second list item.
*	And here's the third list item.

	
### 引用块
```

	* 　This is the first list item.
	* 　Here's the second list item.
	　　> A blockquote would look great below the second list item.
	* 　And here's the third list item.


```
渲染效果如下：

*	This is the first list item.
*	Here's the second list item.
		> A blockquote would look great below the second list item.
*	And here's the third list item.

### 代码块
代码块通常采用四个空格或一个制表符缩进。当它们被放在列表中时，请将它们缩进八个空格或两个制表符。
```

	1. Open the file.`
	2. Find the following code block on line 21:`
	
		<html>
			<head>
				<title>Test</title>
			</head>
	3. Update the title to match the name of your website.


```

渲染效果如下：

1. Open the file.
2. Find the following code block on line 21:

		<html>
			<head>
				<title>Test</title>
			</head>
3. Update the title to match the name of your website.

### 图片
```

1. Open the file containing the Linux mascot.
2. Marvel at its beauty.
	![Tux, the Linux mascot](/assets/images/tux.png)
3. Close the file.


```
渲染效果如下：

1. Open the file containing the Linux mascot.
2. Marvel at its beauty.
	![tux.png](https://s2.loli.net/2024/06/09/YHUbE9JCwoWTBeV.png)
3. Close the file.

### 列表

您可以将无序列表嵌套在有序列表中，反之亦然。
```

1. First item
2. Second item
3. Third item
	- Indented item
	- Indented item
4. Fourth item


```
渲染效果如下：

1. First item
2. Second item
3. Third item
	- Indented item
	- Indented item
4. Fourth item

