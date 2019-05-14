---
layout: post
title: "debian9删除多余开机启动项"
date: 2018-11-06
author: jjnoob
categories:
- 2018-11
tags:
- linux
---

> ### 也就两条命令，很简单。当然也可以通过PE来删除多余的开机启动项

```bash
sudo efibootmgr  //显示efi的启动项

sudo efibootmgr -b 000C -B  //删除多余的启动项,其中000C是要删除的引导项编号
```
![img](/screenshots/linuxbootmgr01.png)

> ## END

Thanks！

https://jingyan.baidu.com/article/67508eb426c8ad9ccb1ce445.html

