---
layout: post
title: "华硕电脑玄学装ubuntu"
date: 2018-11-04
author: jjnoob
categories:
- 2018-11
tags:
- install
---

> ### 玄学至上

周六晚给别人装Ubuntu，不得不说这台笔记本电脑太狗血了，我给他装debian,ubuntu,deepin都能正常安装但是 重启 登陆 后就没反应。。。。。。。。

一直从周六晚上捣鼓到周日晚，其他事啥也没做。。。。。。。。。。。。

他有一块1tb的机械硬盘和一块120gb的固态硬盘。

将Ubuntu安装在那块机械硬盘里面，更改配置也没有用，完全是玄学。

但是将Ubuntu装在固态硬盘里面更改配置后就可以了，不要问我为什么，玄学。

### 该电脑配置如下：

![img](/screenshots/ubuntu-desktop-gouxue.png)

> ## 分界线

因为他要装的是双系统，而且由于玄学原因，我将Windows10装在了机械硬盘里面(无奈之举，之前想把win10装在固态里面的，奈何。。。)，然后将ubuntu装在固态里面。

### 1，正常安装，没什么好说的

### 2，重启进入 > Ubuntu高级选项 > recovery > root 

### 3, 进入tty下
```bash
ctrl + alt + F1  //F1-F6都行

cd ~

ls -al

rm -rf .Xaut*
```

### 4,再次进入ubuntu里面发现可以正常登陆，可以进入桌面里面，但是使用诸如shutdown等命令会出现卡死的现象，这是双显卡驱动不兼容的问题，装上nvida的闭源驱动即可。

### 5,配置双系统时间差异，没什么好说的。done.

> ## END


