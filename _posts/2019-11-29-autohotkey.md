---
layout: post
title: "cap + hjkl"
date: 2019-11-29
author: jjnoob
categories:
- 2019-11
tags:
- keymap
---

* content
{:toc}


用cap + hjkl分别表示 左下上又. 

新建`ahk`后缀的文件, 输入以下内容:

```
CapsLock & j::
   Send, {Down}
Return

CapsLock & l::
   Send, {Right}
Return

CapsLock & h::
   Send, {Left}
Return

CapsLock & k::
   Send, {Up}
Return
```

保存, 双击运行该脚本即可.
