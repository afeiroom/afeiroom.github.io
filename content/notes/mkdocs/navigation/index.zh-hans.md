---
title: 导航设置
description: "在 MkDocs 中启用导航标签，设置相关导航标签功能。"
# linkTitle:
date: 2024-04-13T19:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 4
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
  - https://s2.loli.net/2024/05/11/YFpZ3hjOJdWTrNS.jpg?width=1920&height=1440
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

# 导航设置
	
第一天新搭建网站时无脑设置了一些导航特性，今天研究一下都是干什么用的。

当时的设置如下：
```

theme:
  features:
    - navigation.tabs
    - navigation.tabs.sticky
    - navigation.sections
    - navigation.indexes
    - navigation.instant
    - navigation.instant.progress
    - navigation.tracking
    - navigation.path
    - toc.integrate
    - navigation.top
    - header.autohide
    - announce.dismiss
    - content.action.edit
	
```

## 导航标签


启用导航标签后，顶级部分将呈现在标题下方的菜单图层中，用于上面的视区，但在移动设备上保持原样。将以下行添加到：`mkdocs.yml`文件

```

theme:
  features:
    - navigation.tabs
	
```

带导航标签
![带导航标签](https://s2.loli.net/2024/05/13/vMt4UcqDEa59YF6.png)

不带导航标签
![不带导航标签](https://s2.loli.net/2024/05/13/v1RQGChtE9maT7g.png)

## 粘性导航标签

启用粘滞导航标签后，导航标签将锁定在标题下方，并在向下滚动时始终保持可见。只需将以下两个功能标志添加到：mkdocs.yml
```

theme:
  features:
    - navigation.tabs
    - navigation.tabs.sticky


```

带粘性导航标签
![带粘性导航标签](https://s2.loli.net/2024/05/13/iryVWaDMXEcIh86.png)

不带粘性导航标签
![不带粘性导航标签](https://s2.loli.net/2024/05/13/8CvdB3mM75Gi9fP.png)

## 导航分区
启用导航分区后，顶级分区将在上面视口的边栏中呈现为组，但在移动设备上保持原样。将以下行添加到：mkdocs.yml
```

theme:
  features:
    - navigation.sections
	
```

注意：此功能效果只有在导航分了章节才能体现，例如：
```

nav:
  - ChatGLM:
    - 第一部分:
      - chatglm/page1-1.md
      - chatglm/page1-2.md
    - 第二部分:
      - chatglm/page2-1.md
      - chatglm/page2-2.md
    - 第三部分:
      - chatglm/page3-1.md
      - chatglm/page3-2.md
	
```
带导航分区
![带导航分区](https://s2.loli.net/2024/05/13/DdXvhmZlqwH8cxe.png)

不带导航分区
![不带导航分区](https://s2.loli.net/2024/05/13/nMJsNz7Q4mex6VW.png)

## 导航扩展

启用扩展后，左侧边栏将默认展开所有可折叠的子部分，因此用户不必手动打开小部分。将以下行添加到：mkdocs.yml
```

theme:
  features:
    - navigation.expand
	
```

带导航扩展

![带导航扩展](https://s2.loli.net/2024/05/13/MHafmhb4rKuDzLc.png)

不带导航扩展

![不带导航扩展](https://s2.loli.net/2024/05/13/Rtz1HJlPueO6rmk.png)

## 章节索引页

启用章节索引页后，文档可以直接附加到节，这对于提供概述页特别有用。将以下行添加到：mkdocs.yml
```

theme:
  features:
    - navigation.indexes
	
```


要将页面链接到某个部分，请在相应的文件夹中创建一个名称为新文档，并将其添加到导航部分的开头：index.md
```

nav:
  - Section:
    - section/index.md 
    - Page 1: section/page-1.md
    ...
    - Page n: section/page-n.md
	
```

## 目录锚点跟踪

启用目录的锚点跟踪后，目录边栏将自动滚动，以便活动锚点始终可见。将以下行添加到：mkdocs.yml
```

theme:
  features:
    - toc.follow
	
```

## 目录导航集成

启用目录导航集成后，它始终呈现为左侧导航侧边栏的一部分。将以下行添加到：mkdocs.yml
```

theme:
  features:
    - toc.integrate
	
```

## 返回顶部按钮

当用户向下滚动后再次开始向上滚动时，可以显示返回顶部按钮。它呈现在标题的中心和正下方。将以下行添加到：mkdocs.yml
```

theme:
  features:
    - navigation.top
	
```

## 隐藏侧边栏

对于具有 front matter 属性的文档，可以隐藏导航和/或目录侧边栏。在 Markdown 文件的顶部添加以下行：hide
```

---
hide:
  - navigation
  - toc
---

# Page title
...


```







