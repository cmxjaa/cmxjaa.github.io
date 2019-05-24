---
layout: post
title: "hackinglab-xss"
date: 2019-05-23
author: jjnoob
categories:
- 2019-05
tags:
- xss
---

* content
{:toc}


> 待更新, 先去看计网.


> 还是hackinglab
[参考](https://www.cnblogs.com/renzongxian/p/5618631.html)


# 一. key又又找不到了

点击链接, 跳转后抓包. 查看response包, 发现:
```
<script>window.location="./no_key_is_here_forever.php"; </script>
key is : yougotit_script_now
```

# 二. 快速口算
[代码参考](https://www.cnblogs.com/renzongxian/p/5618631.html)

```py
#!/usr/bin/env python3
# Author: renzongxian

import requests
import re
url = 'http://lab1.xseclab.com/xss2_0d557e6d2a4ac08b749b61473a075be1/index.php'
header = {'Cookie': 'PHPSESSID=$Your Cookie'}
    
# 获取算式
resp_content = requests.get(url, headers = header).content.decode('utf-8')
matches = re.search("(.*)=<input", resp_content)
# 发送结果
# 提交数据也是键值对形式, 根据源码中的<input type="text" name="v">可知下行中v的由来
data = {'v': str(eval(matches.group(1)))}
resp_content = requests.post(url, headers=header, data=data).content.decode('utf-8')
# 取得响应内容
matches = re.search("<body>(.*)</body>", resp_content)
print(matches.group(1))
```

## python
> 学的不是很好


### 正则表达式
[参考](https://blog.csdn.net/lfeng1205/article/details/52058674)


* `(.*)`正则表达式 
`(.*)`涉及到贪婪模式。当正则表达式中包含能接受重复的限定符时，通常的行为是（在使整个表达式能得到匹配的前提下）匹配尽可能多的字符。以这个表达式为例：`a.*b`，它将会匹配最长的以`a`开始，以`b`结束的字符串。如果用它来搜索`aabab`的话，它会匹配整个字符串`aabab`。这被称为贪婪匹配。

* `(.*?)`正则表达式 
懒惰匹配，也就是匹配尽可能少的字符。就意味着匹配任意数量的重复，但是在能使整个匹配成功的前提下使用最少的重复。`a.?b` 匹配最短的，以`a`开始，以`b`结束的字符串。如果把它应用于`aabab`的话，它会匹配`aab`（第一到第三个字符）和`ab`（第四到第五个字符）。

### `matches.group()`
`group`是针对 `()` 来说的，`group(0)`就是指的整个串，`group(1)` 指的是第一个括号里的东西，`group(2)`指的第二个括号里的东西。

### `eval()`
eval() 函数用来执行一个字符串表达式，并返回表达式的值。


<br />

# 三. 这个题目是空的

输入`null`就行了..


<br />

# 四. 怎么就是不弹出key呢?
> 图书馆的空调怕是想冻死我...


flag: `slakfjteslkjsd`

1. 查看网页源代码发现点击链接会触发 JS 代码中的函数`a()`, 但是 JS 代码中有三个 `return false;` 的函数导致函数 `a()` 失效.
2. 将代码完整复制到本地的html文件，然后把 `<script>` 标签那3个干扰的函数删除, 最后在浏览器里打开就可以弹窗了.

<br />

# 五. 逗比验证码第一期
根据题目提示, 验证码不会过期. 输入密码和验证码, burp抓包爆破即可.

## 关于burp爆破
针对本题熟悉一下burp爆破的步骤:
[参考](https://blog.csdn.net/yalecaltech/article/details/69056210)


1. 输入密码和验证码, 提交.
2. burp抓包. `send to intruder`.
3. burp会默认将所有可能需要爆破的量都用`$`做标记, 所以我们需要先点击右边的`clear` 清除所有的 `$`, 然后选中我们想要爆破的量也就是`pwd`后面的值，点击`add`进行标记.
4. `payload sets`设定字典类型, 这里选择`numbers`.
5. 根据题目提示, 设定`payload options`的数字范围为从`1000-9999`, `step`为`1`. 
6. 为了让速度更快, 设定线程数为`10`. `options` -> `request engine` -> `number of threads` 为`10`.
7. 选择左上角`instruder` -> `start attack`进行爆破.
8. 爆破结束后主要看页面中的`length`, 不一样的就是成功登陆的，通过下面的`response`我们可以看到登陆成功后返回的信息，在这里也就得到了`key`. 


<br />

# 六. 逗比验证码第二期
验证便失效的验证码

根据网上的思路就是既然验证码失效, 那就直接设置包里面的验证码值为空, 这里是`vcode`的值为空.
```
username=admin&pwd§=admin§&vcode=&submit=submit
```

步骤与第五题一样, 爆破得到key.

<br />

# 七. 逗比的验证码第三期（SESSION）
加入了 session 验证，把 cookies 的内容删掉就好.

> 由于HTTP协议是无状态的协议，所以服务端需要记录用户的状态时，就需要用某种机制来识具体的用户，这个机制就是Session.

修改部分:
```
Cookie: PHPSESSID=


username=admin&pwd=§admin§&vcode=&submit=submit
```

剩下步骤和前两题一样, 用burp爆破.

<br />

# 八. 微笑一下就能过关了
[参考](https://blog.csdn.net/qq_26090065/article/details/82503651)

[参考](https://www.waitalone.cn/security-scripts-game.html)

## (1) 源码
查看源码, 观察发现:
```html
<form name="login" action="index.php" method="POST" accept-charset="utf-8"> 
    <ul> 
        <li> 
            <label for="SMILE">请使用微笑过关<a href="?view-source">源代码</a></label> 
            <input type="text" name="T_T" placeholder="where is your smile" required> 
        </li> 
        <li><input type="submit" value="Show"> </li> 
    </ul> 
</form> 
```

地址栏访问:`?view-source`. 得到php源码.
```php
<?php  
    header("Content-type: text/html; charset=utf-8");
    if (isset($_GET['view-source'])) { 
        show_source(__FILE__); 
        exit(); 
    } 
 
    include('flag.php'); 
 
    $smile = 1;  
 
   if (!isset ($_GET['^_^'])) $smile = 0;  
    if (preg_match ('/\./', $_GET['^_^'])) $smile = 0;  
    if (preg_match ('/%/', $_GET['^_^'])) $smile = 0;  
    if (preg_match ('/[0-9]/', $_GET['^_^'])) $smile = 0;  
    if (preg_match ('/http/', $_GET['^_^']) ) $smile = 0;  
    if (preg_match ('/https/', $_GET['^_^']) ) $smile = 0;  
    if (preg_match ('/ftp/', $_GET['^_^'])) $smile = 0;  
    if (preg_match ('/telnet/', $_GET['^_^'])) $smile = 0;  
    if (preg_match ('/_/', $_SERVER['QUERY_STRING'])) $smile = 0; 
    if ($smile) { 
        if (@file_exists ($_GET['^_^'])) $smile = 0;  
    }  
    if ($smile) { 
        $smile = @file_get_contents ($_GET['^_^']);  
        if ($smile === "(●'◡'●)") die($flag);  
    }  
?>
```

## (2) 需要满足条件
发现需要满足的条件有:

1. 必须对`^_^`赋值
2. `^_^`的值不能有  `.`  `%`  `[0-9]`  `http`  `https`  `ftp`  `telnet`  这些东西
3. `$_SERVER['QUERY_STRING']`,即`^_^=(输入的值)`这个字符串不能有`_` 这个字符
4. 满足`$smile!=0`
5. `file_exists ($_GET['^_^'])`必须为0.也就是`$_GET['^_^']`此文件不存在
6. `$smile`必须等于`(●'◡'●)`.也就是`file_get_contents($_GET['^_^'])`必须为`(●'◡'●)`


## (3) 矛盾与解决
### 逻辑矛盾处:
1. `QUREY_STRING`过滤了`_`但是`$_GET[‘^_^’]`又含有`_`.
2. `file_exists`需要寻找的文件必须不存在, 但`file_get_contents却能读取到文件内容.


### 分析
1. 可以采用Url编码变为`%5f`. 这样第3点就满足了. 所以我们输入就应该为`^%5f^`
2. `file_get_contents`可以获取远程数据, 但常用网络协议已经被正则过滤, 因此需要选取其他协议. 而在php支持的协议和包装中, `RFC 2397`的`data`协议可用. 并且, `file_exists`对于`data`指向内容判断为不存在.



最后构造: `^%5f^=data:,(●'◡'●)`, 即url输入`?^%5f^=data:,(●'◡'●)`. 即可以得到flag.

<br />

# 九.逗比的手机验证码
跟着步骤来就行. 注意获得验证码并返回后, 不仅要填写验证码也要修改手机号.


<br />

