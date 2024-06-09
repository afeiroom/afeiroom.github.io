---
title: Markdown 转义字符语法
description: "要显示原本用于格式化 Markdown 文档的字符，请在字符前面添加反斜杠字符 \ 。"
# linkTitle:
date: 2024-04-11T12:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 12
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
  - https://s2.loli.net/2024/06/09/bLSf6mixNRtTj9D.jpg?width=1920&height=1440
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

# Markdown 转义字符语法
要显示原本用于格式化 Markdown 文档的字符，请在字符前面添加反斜杠字符 \ 。
```

	\* Without the backslash, this would be a bullet in an unordered list.
	
```
渲染效果如下：

\* Without the backslash, this would be a bullet in an unordered list.

## 可做转义的字符
以下列出的字符都可以通过使用反斜杠字符从而达到转义目的。

| 字符  | 名称                                                              |
| :---- | :---------------------------------------------------------------- |
| \     | 反斜线                                                            |
| \`    | 反引号 (另见在代码中转义反引号【Markdown 代码语法 - 转义反引号】) |
| \*    | 星号                                                              |
| \_    | 下划线                                                            |
| \{ \} | 花括号                                                            |
| \[ \] | 方括号                                                            |
| \( \) | 圆括号                                                            |
| \#    | 井号                                                              |
| +     | 加号                                                              |
| -     | 减号 (连字符)                                                     |
| .     | 点                                                                |
| !     | 感叹号                                                            |
| \|    | 管道字符 (另见【Markdown表格 - 在表中转义管道字符】)              |

## 特殊字符自动转义
在 HTML 文件中，有两个字符需要特殊处理： `<` 和 `&` 。 `<` 符号用于起始标签，`&` 符号则用于标记 HTML 实体，如果你只是想要使用这些符号，你必须要使用实体的形式，像是 `&lt;` 和` &amp;`。

`&` 符号其实很容易让写作网页文件的人感到困扰，如果你要打「AT&T」 ，你必须要写成「`AT&amp;T`」 ，还得转换网址内的 `&` 符号，如果你要链接到：
```

	http://images.google.com/images?num=30&q=larry+bird
	
```

你必须要把网址转成：
```

	http://images.google.com/images?num=30&amp;q=larry+bird
	
```

才能放到链接标签的 `href` 属性里。不用说也知道这很容易忘记，这也可能是 HTML 标准检查所检查到的错误中，数量最多的。

Markdown 允许你直接使用这些符号，它帮你自动转义字符。如果你使用 `&` 符号的作为 HTML 实体的一部分，那么它不会被转换，而在其它情况下，它则会被转换成 `&amp;`。所以你如果要在文件中插入一个著作权的符号，你可以这样写：
```

	&copy;
	
```

&copy;

Markdown 将不会对这段文字做修改，但是如果你这样写：
```

	AT&T
	
```

Markdown 就会将它转为：
```

	AT&amp;T
	
```

类似的状况也会发生在 `<` 符号上，因为 Markdown 支持 行内 HTML ，如果你使用 `<` 符号作为 HTML 标签的分隔符，那 Markdown 也不会对它做任何转换，但是如果你是写：
```

	4 < 5
	
```

Markdown 将会把它转换为：
```

	4 &lt; 5
	
```

需要特别注意的是，在 Markdown 的块级元素和内联元素中， `<` 和 `&` 两个符号都会被自动转换成 HTML 实体，这项特性让你可以很容易地用 Markdown 写 HTML。（在 HTML 语法中，你要手动把所有的 `<` 和 `&` 都转换为 HTML 实体。）

