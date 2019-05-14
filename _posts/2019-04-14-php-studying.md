---
layout: post
title: "PHP-Studying"
date: 2019-04-14
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> 刷了bugku几题, 发现要用PHP....于是过来简单看看, 熟悉基本语法

[参考](http://www.w3school.com.cn/php/index.asp)

# 一. PHP 变量
### (1) PHP 变量作用域

PHP 有三种不同的变量作用域：
* local（局部）
* global（全局）
* static（静态）

### (2) Local 和 Global 作用域
* 函数之外声明的变量拥有 Global 作用域，只能在函数以外进行访问。
* 函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。

### (3) Global 关键词
global 关键词用于在函数内访问全局变量。
```php
  global $x,$y;
```

PHP 同时在名为 `$GLOBALS[index]`的数组中存储了所有的全局变量。下标存有变量名。这个数组在函数内也可以访问，并能够用于直接更新全局变量。

### (4) static 关键词
* 当函数完成/执行后，会删除所有变量。
* 如果需要不删除某个局部变量, 在首次声明变量时使用 static 关键词

<br />

# 二. PHP Echo/Print
### (1) PHP echo 和 print 语句
echo 和 print 之间的差异：
* echo - 能够输出一个以上的字符串
* print - 只能输出一个字符串，并始终返回 1
* echo 比 print 稍快，因为它不返回任何值。

<br />

# 三. PHP 字符串
> 都是一些string的函数

<br />

# 四. PHP 常量
常量是自动全局的，而且可以贯穿整个脚本使用
```php
define("GREETING", "Welcome to W3School.com.cn!"); #对大小写敏感的常量

define("GREETING", "Welcome to W3School.com.cn!", true);  #对大小写不敏感的常量
```

<br />

# 五. PHP 运算符
### PHP 串接运算符:  `.`

```php
<?php
$a = "Hello";
$b = $a . " world!";
echo $b; // 输出 Hello world!

?>
```

<br />

# 六. PHP for 循环
### PHP foreach 循环
foreach 循环只适用于数组，并用于遍历数组中的每个键/值对

```php
<?php 
$colors = array("red","green","blue","yellow"); 

foreach ($colors as $value) {
  echo "$value <br>";
}
?>
```
输出:
```
red 
green 
blue 
yellow 
```

<br />

# 七. PHP 函数
### (1) 用户定义函数
```php
<?php
function sayHi() {  //创建函数
  echo "Hello world!";
}

sayhi(); // 调用函数
?>
```

### (2) 默认参数值
```php
function setHeight($minheight=50) {
  echo "The height is : $minheight <br>";
}
```

<br />

# 八. PHP 数组
### (1) 实例:
```php
<?php
$cars=array("porsche","BMW","Volvo");
echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".";
?>
```

### (2) 关联数组
创建方法一:
```php
$age=array("Bill"=>"35","Steve"=>"37","Elon"=>"43");
```
创建方法二:
```php
$age['Bill']="63";
$age['Steve']="56";
$age['Elon']="47";
```
<br />

使用:
```php
<?php
$age=array("Bill"=>"63","Steve"=>"56","Elon"=>"47");
echo "Elon is " . $age['Elon'] . " years old.";
?>
```
输出:
```
Elon is 47 years old.
```

<br />

# 九. PHP 全局变量 - 超全局变量
PHP 中的许多预定义变量都是“超全局的”，这意味着它们在一个脚本的全部作用域中都可用。在函数或方法中无需执行 global $variable; 就可以访问它们。

这些超全局变量是：
```php
$GLOBALS
$_SERVER
$_REQUEST
$_POST
$_GET
$_FILES
$_ENV
$_COOKIE
$_SESSION
```

### (1) `$GLOBALS` — 引用全局作用域中可用的全部变量
`$GLOBALS`这种全局变量用于在 PHP 脚本中的任意位置访问全局变量（从函数或方法中均可）。

PHP 在名为 `$GLOBALS[index]` 的数组中存储了所有全局变量。变量的名字就是数组的键。

### (2) PHP `$_SERVER`
`$_SERVER` 这种超全局变量保存关于报头、路径和脚本位置的信息。

### (3) PHP `$_REQUEST`
`PHP $_REQUEST` 用于收集 HTML 表单提交的数据。

点击提交按钮时, 表单数据发送到 PHP文件本身:
```html
<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
Name: <input type="text" name="fname">
<input type="submit">
</form>
```
使用超级全局变量 `$_REQUEST` 来收集 input 字段的值：
```php
<?php 
$name = $_REQUEST['fname']; 
echo $name; 
?>
````

### (4) PHP $_POST
PHP `$_POST` 广泛用于收集提交 `method="post"` 的 HTML 表单后的表单数据。`$_POST` 也常用于传递变量。

```html
<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
Name: <input type="text" name="fname">
<input type="submit">
</form>
```

```php
$name = $_POST['fname'];
```

### (5) PHP `$_GET`
PHP `$_GET` 也可用于收集提交 HTML 表单 (`method="get"`) 之后的表单数据。

`$_GET` 也可以收集 URL 中的发送的数据。

当用户点击链接 "测试 `$GET`"，参数 "subject" 和 "web" 被发送到 "test_get.php"，然后就能通过 `$_GET` 在 "test_get.php" 中访问这些值了: 
```html
<a href="test_get.php?subject=PHP&web=W3school.com.cn">测试 $GET</a>
```
"test_get.php" 中的代码：
```php 
echo "在 " . $_GET['web'] . " 学习 " . $_GET['subject'];
```


