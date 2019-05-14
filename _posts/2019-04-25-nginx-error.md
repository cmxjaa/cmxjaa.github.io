---
layout: post
title: "nginx报错总结"
date: 2019-04-26
author: jjnoob
category: 2019-04
tags: nginx
finished: true
---

> 希望能把nginx的报错都总结起来.

# 一. 报错, 忘了, nginx is not active之类的.
[参考](https://yq.aliyun.com/articles/44661)

解决方法:
### Nginx的启动
```
/usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf  
```
### 另: Nginx的重加载
```
/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
```
