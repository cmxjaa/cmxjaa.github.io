---
layout: post
title: "修改Blog代码区颜色"
date: 2019-03-31
author: duckduckk
category: 2019-03
tags: blog
finished: true
---

> 老早就觉得博文代码区颜色很丑,一直想改...


# 修改code区颜色
CSS文档地址: `/public/stylesheets/pyment_trac.css`

原代码块中代码为红色, 背景为白色.
```css
code{
color: #bf616a;
backgroud-color: #f9f9f9;
}
```

修改为代码为绿色, 背景为黑色
```css
code{
color: #00FF00;
backgroud-color: #1D1D1F;
}
```

修改后效果如下:
`debian`

<br/>

# 修改错误代码的颜色及背景
地址: `/public/stylesheets/pygment_trac.css`

由灰底红字改为 黑底鲜红字

原代码:
```css
.highlight .err { color: #a61717; background-color: #e3d2d2 } /* Error */
```
修改后:
```css
.highlight .err { color: #FF0000; background-color: #1D1D1F } /* Error */
```
