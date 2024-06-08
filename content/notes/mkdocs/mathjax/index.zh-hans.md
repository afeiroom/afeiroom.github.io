---
title: 数学扩展
updated: 2024-04-13 11:10:48Z
created: 2024-04-13 01:52:34Z
latitude: 28.68289200
longitude: 115.85819800
altitude: 0.0000

description: "配置支持使用 MathJax 和 KaTeX 渲染块和内联块方程。"
# linkTitle:
date: 2024-04-13T21:00:00+08:00
draft: false
noindex: false
featured: false
pinned: false
nav_weight: 6
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
  - https://s2.loli.net/2024/05/11/GXpVCSad2hDyQuA.jpg?width=1920&height=1440
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

# 数学扩展

MathJax 和 KaTeX 是两个流行的库，用于在浏览器中显示数学内容。尽管这两个库提供类似的功能，但它们使用不同的语法并具有不同的配置选项。此文档站点提供了有关如何轻松地将它们与 Material for MkDocs 集成的信息。

## 配置
以下配置支持使用 MathJax 和 KaTeX 渲染块和内联块方程。

### MathJax
MathJax 是一个功能强大且灵活的库，支持多种输入格式，例如 LaTeX、MathML、AsciiMath，以及各种输出格式，例如 HTML、SVG、MathML。要在项目中使用 MathJax，请将以下行添加到您的 .mkdocs.yml

文件mkdocs.yml
```

markdown_extensions:
  - pymdownx.arithmatex:
      generic: true

extra_javascript:
  - javascripts/mathjax.js
  - https://polyfill.io/v3/polyfill.min.js?features=es6
  - https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js
  
 ```
 
文件 docs/javascripts/mathjax.js
```

window.MathJax = {
  tex: {
    inlineMath: [["\\(", "\\)"]],
    displayMath: [["\\[", "\\]"]],
    processEscapes: true,
    processEnvironments: true
  },
  options: {
    ignoreHtmlClass: ".*|",
    processHtmlClass: "arithmatex"
  }
};

document$.subscribe(() => { 
  MathJax.startup.output.clearCache()
  MathJax.typesetClear()
  MathJax.texReset()
  MathJax.typesetPromise()
})

```

请参阅其他配置选项：

[Arithmatex](https://squidfunk.github.io/mkdocs-material/setup/extensions/python-markdown-extensions/#arithmatex)

### KaTeX

KaTeX 是一个轻量级库，专注于速度和简单性。它支持 LaTeX 语法的子集，并且可以将数学呈现为 HTML 和 SVG。要在项目中使用 KaTeX，请将以下行添加到您的 .mkdocs.yml


文件mkdocs.yml
```

markdown_extensions:
  - pymdownx.arithmatex:
      generic: true

extra_javascript:
  - javascripts/katex.js
  - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/katex.min.js
  - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/contrib/auto-render.min.js

extra_css:
  - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/katex.min.css
  
 ```
 
文件 docs/javascripts/katex.js
```

document$.subscribe(({ body }) => { 
  renderMathInElement(body, {
    delimiters: [
      { left: "$$",  right: "$$",  display: true },
      { left: "$",   right: "$",   display: false },
      { left: "\\(", right: "\\)", display: false },
      { left: "\\[", right: "\\]", display: true }
    ],
  })
})

```

