---
title: Markdown 引用语法
description: "要创建块引用，请在段落前添加一个 > 符号。"
# linkTitle:
date: 2024-04-11T06:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 6
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
  - https://s2.loli.net/2024/06/09/ljxseUYPfWztM6a.jpg?width=1920&height=1440
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

# Markdown 引用语法

要创建块引用，请在段落前添加一个 `>` 符号。

```

	> Dorothy followed her through many of the beautiful rooms in her castle.>


```
渲染效果如下所示：

> Dorothy followed her through many of the beautiful rooms in her castle.

## 多个段落的块引用

块引用可以包含多个段落。为段落之间的空白行添加一个 `>` 符号。

```

	> Dorothy followed her through many of the beautiful rooms in her castle.
	> 
	> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.


```

渲染效果如下：
> Dorothy followed her through many of the beautiful rooms in her castle.
> 
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

## 嵌套块引用

块引用可以嵌套。在要嵌套的段落前添加一个 `>>` 符号。
```

	> Dorothy followed her through many of the beautiful rooms in her castle.
	> 
	>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.


```
渲染效果如下：

> Dorothy followed her through many of the beautiful rooms in her castle.
> 
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

## 带有其它元素的块引用

块引用可以包含其他 Markdown 格式的元素。并非所有元素都可以使用，你需要进行实验以查看哪些元素有效。
```

> #### The quarterly results look great!
> 
> - Revenue was off the chart.
> - Profits were higher than ever.
> 
> *Everything* is going according to **plan**.


```
渲染效果如下：

> #### The quarterly results look great!
> 
> - Revenue was off the chart.
> - Profits were higher than ever.
> 
> *Everything* is going according to **plan**.

