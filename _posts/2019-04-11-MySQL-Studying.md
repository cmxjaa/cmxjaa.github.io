---
layout: post
title: "MySQL-Studying"
date: 2019-04-11
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> MySQL数据库.

[参考菜鸟教程](http://www.runoob.com/mysql/mysql-tutorial.html)

# 一. MySQL 教程
### (1) 什么是数据库
RDBMS (关系数据库管理系统) 的特点：
* 数据以表格的形式出现
* 每行为各种记录名称
* 每列为记录名称所对应的数据域
* 许多的行和列组成一张表单
* 若干的表单组成database

### (2) RDBMS 术语
#### RDBMS的一些术语：
* 数据库: 数据库是一些关联表的集合。
* 数据表: 表是数据的矩阵。在一个数据库中的表看起来像一个简单的电子表格。
* 列: 一列(数据元素) 包含了相同的数据, 例如邮政编码的数据。
* 行：一行（=元组，或记录）是一组相关的数据，例如一条用户订阅的数据。
* 冗余：存储两倍数据，冗余降低了性能，但提高了数据的安全性。
* 主键：主键是唯一的。一个数据表中只能包含一个主键。你可以使用主键来查询数据。
* 外键：外键用于关联两个表。
* 复合键：复合键（组合键）将多个列作为一个索引键，一般用于复合索引。
* 索引：使用索引可快速访问数据库表中的特定信息。索引是对数据库表中一列或多列的值进行排序的一种结构。类似于书籍的目录。
* 参照完整性: 参照的完整性要求关系中不允许引用不存在的实体。与实体完整性是关系模型必须满足的完整性约束条件，目的是保证数据的一致性。



#### 一个关系型数据库由一个或数个表格组成, 表格里面的相关概念:
* 表头(header): 每一列的名称;
* 列(col): 具有相同数据类型的数据的集合;
* 行(row): 每一行用来描述某条记录的具体信息;
* 值(value): 行的具体信息, 每个值必须与该列的数据类型相同;
* 键(key): 键的值在当前列中具有唯一性。

> 教程上说学习MySQL需要HTML和PHP的基础. PHP我就看了一点点. 应该没有多大影响....吧

<br />

# 二. MySQL 安装
[看一下就行](http://www.runoob.com/mysql/mysql-install.html)

# 三. MySQL 管理
> 我电脑装的是 lnmp. 和直接装MySQL的话, 命令有些不同. 所以有些命令执行不了, 并没有什么大问题, 直接跳过.

### (1) MySQL 用户设置
>　看 三(2)

### (2) 管理MySQL的命令
1. USE 数据库名：
选择要操作的Mysql数据库，使用该命令后所有Mysql命令都只针对该数据库。
```sql
mysql> use RUNOOB;
```

2. SHOW DATABASES: 
列出 MySQL 数据库管理系统的数据库列表。
```sql
mysql> SHOW DATABASES;
```

3. SHOW TABLES:
显示指定数据库的所有表，使用该命令前需要使用 use 命令来选择要操作的数据库。
```sql
mysql> use RUNOOB;
Database changed
mysql> SHOW TABLES;
```

4. SHOW COLUMNS FROM 数据表:
显示数据表的属性，属性类型，主键信息 ，是否为 NULL，默认值等其他信息。
```sql
mysql> SHOW COLUMNS FROM runoob_tbl;
```

5. SHOW INDEX FROM 数据表:
显示数据表的详细索引信息，包括PRIMARY KEY（主键）。
```sql
mysql> SHOW INDEX FROM runoob_tbl;
```

6. SHOW TABLE STATUS LIKE [FROM db_name] [LIKE 'pattern'] \G: 
该命令将输出Mysql数据库管理系统的性能及统计信息
```sql
mysql> SHOW TABLE STATUS  FROM RUNOOB;   # 显示数据库 RUNOOB 中所有表的信息
mysql> SHOW TABLE STATUS from RUNOOB LIKE 'runoob%';     # 表名以runoob开头的表的信息
mysql> SHOW TABLE STATUS from RUNOOB LIKE 'runoob%'\G;   # 加上 \G，查询结果按列打印
```

# 三(２) MySQL 用户设置
>　原教程在这一块不如我之前看过的一篇教程说的明白


[参考链接](https://www.cnblogs.com/chanshuyi/p/mysql_user_mng.html)

### (1) 新建用户
1. root登录
2. 创建用户zhangsan, 密码为zhangsanpsw: 
    ```sql
    mysql> create user zhangsan identified by 'zhangsanpwd';
    ```
    
    
3. 可以在mysql.user表里看到新增用户的信息:
    ```sql
    mysql> select User,Host,Password from mysql.user where User = 'zhangsan';
    ```

### (2) 授权
1. 授权:
    ```sql
    create database zhangsanDb; # 先要创建数据库
    grant all privileges on zhangsanDb.* to zhangsan@'%' identified by 'zhangsan';
    flush privileges;  # 刷新权限变更
    ```

2. 可以通过show grants命令查看权限授予执行的命令：
    ```sql
    show grants for 'zhangsan';
    ```
    
3. privilegesCode表示授予的权限类型，常用的有以下几种类型:
* all privileges：所有权限。
* select：读取权限。
* delete：删除权限。
* update：更新权限。
* create：创建权限。
* drop：删除数据库、数据表权限。

4. dbName.tableName表示授予权限的具体库或表，常用的有以下几种选项：

* `.`：授予该数据库服务器所有数据库的权限。
* `dbName.*`：授予dbName数据库所有表的权限。
* `dbName.dbTable`：授予数据库dbName中dbTable表的权限。

5. username@host表示授予的用户以及允许该用户登录的IP地址。其中Host有以下几种类型：

* `localhost`：只允许该用户在本地登录，不能远程登录。
* `%`：允许在除本机之外的任何一台机器远程登录。
* `192.168.52.32`：具体的IP表示只允许该用户从特定IP登录。

6. password指定该用户登录时的面。

7. flush privileges 表示刷新权限变更。

### (3) 修改密码
```sql
update mysql.user set password = password('zhangsannew') where user = 'zhangsan' and host = '%';
flush privileges;
```

### (4) 删除用户
```sql
drop user zhangsan@'%';
```

### (5) 常用命令组
创建用户并授予指定数据库全部权限：适用于Web应用创建MySQL用户
```sql
create user zhangsan identified by 'zhangsan';
grant all privileges on zhangsanDb.* to zhangsan@'%' identified by 'zhangsan';
flush  privileges;
```

<br />

# 四. MySQL PHP 语法
Mysql在PHP的web开发中是应用最广泛
>　难道我要放下mysql,　先去看php? 

PHP Mysqli函数格式如下：
```php
mysqli_function(value,value,...); 
```
以上格式中 function部分描述了mysql函数的功能，如
```php
mysqli_connect($connect);
mysqli_query($connect,"SQL 语句");
mysqli_fetch_array()
mysqli_close()
```

<br />

# 五. MySQL 连接
### (1) 使用mysql二进制方式连接
```sql
mysql -u root -p
```

### (2) 使用 PHP 脚本连接 MySQL
PHP 提供了 mysqli_connect() 函数来连接数据库。

该函数有 6 个参数，在成功链接到 MySQL 后返回连接标识，失败返回 FALSE 

语法:
```php
mysqli_connect(host,username,password,dbname,port,socket);
```

参数说明：
* host	规定主机名或 IP 地址。
* username	规定 MySQL 用户名。
* password	规定 MySQL 密码。
* dbname	规定默认使用的数据库。
* port	规定尝试连接到 MySQL 服务器的端口号。
* socket	规定 socket 或要使用的已命名 pipe。

### (3) PHP 连接实例
> php die() 函数输出一条消息，并退出当前脚本。


```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('Could not connect: ' . mysqli_error());
}
echo '数据库连接成功！';
mysqli_close($conn);
?>
```
> 自己敲了一遍, 执行成功了.

<br /> 

# 六. MySQL 创建数据库
### (1) 二进制
#### 使用`create`命令创建: 
```sql
mysql> create DATABASE RUNOOB;
```

#### 使用 mysqladmin 创建数据库: 
宿主机root用户执行命令
```shell
[root@host]# mysqladmin -u root -p create RUNOOB
```

> mysqladmin 我没有执行成功, 不知道是不是 lnmp 的问题.

### (2) 使用 PHP 脚本
> mysqli_close() 函数用来断开与MySQL数据库的链接, 但是通常不需要使用 mysqli_close()，因为已打开的非持久连接会在脚本执行完毕后自动关闭


```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
  die('连接错误: ' . mysqli_error($conn));
}
echo '连接成功<br />';
$sql = 'CREATE DATABASE RUNOOB';
$retval = mysqli_query($conn,$sql );
if(! $retval )
{
    die('创建数据库失败: ' . mysqli_error($conn));
}
echo "数据库 RUNOOB 创建成功\n";
mysqli_close($conn);
?>
```
> 敲了一遍, 成功了

<br />

# 七. MMySQL 删除数据库
### (1) drop 命令删除数据库

```sql
mysql> drop database RUNOOB;
```

### (2) 使用 mysqladmin 删除数据库
```shell
[root@host]# mysqladmin -u root -p drop RUNOOB
```

### (3) 使用PHP脚本删除数据库
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
echo '连接成功<br />';
$sql = 'DROP DATABASE RUNOOB';
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('删除数据库失败: ' . mysqli_error($conn));
}
echo "数据库 RUNOOB 删除成功\n";
mysqli_close($conn);
?>
```

<br />

# 八. MySQL 选择数据库

### (1) 从命令提示窗口中选择MySQL数据库

```sql
mysql> use RUNOOB;
Database changed
```

成功选择了 RUNOOB 数据库，在后续的操作中都会在 RUNOOB 数据库中执行

### (2) 使用PHP脚本选择MySQL数据库
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
echo '连接成功';
mysqli_select_db($conn, 'RUNOOB' );
mysqli_close($conn);
?>
```

<br />

# 九. MySQL 数据类型
MySQL支持多种类型，大致可以分为三类：数值、日期/时间和字符串(字符)类型
>　比较多, 还是需要的时候看教程吧.


### (1) 数值类型
包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)。

### (2) 日期和时间类型
表示时间值的日期和时间类型为DATETIME、DATE、TIMESTAMP、TIME和YEAR。

### (3) 字符串类型
字符串类型指CHAR、VARCHAR、BINARY、VARBINARY、BLOB、TEXT、ENUM和SET。

<br />

# 十. MySQL 创建数据表
创建MySQL数据表需要以下信息：
* 表名
* 表字段名
* 定义每个表字段


### (1) 通过命令提示符创建表
使用 SQL 语句 CREATE TABLE 来创建数据表:
```sql
mysql> use RUNOOB;
Database changed
mysql> CREATE TABLE runoob_tbl(
   -> runoob_id INT NOT NULL AUTO_INCREMENT,
   -> runoob_title VARCHAR(100) NOT NULL,
   -> runoob_author VARCHAR(40) NOT NULL,
   -> submission_date DATE,
   -> PRIMARY KEY ( runoob_id )
   -> )ENGINE=InnoDB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.16 sec)
mysql>
```

* 如果不想字段为 NULL 可以设置字段的属性为 NOT NULL， 在操作数据库时如果输入该字段的数据为NULL ，就会报错。
* AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
* PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
* ENGINE 设置存储引擎，CHARSET 设置编码。
#### 效果:

![img](https://github.com/duckduckk/duckduckk.github.io/blob/master/screenshots/2019-04-10-mysql-table.png?raw=true)

### (2) 使用PHP脚本创建数据表
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
echo '连接成功<br />';
$sql = "CREATE TABLE runoob_tbl( ".
        "runoob_id INT NOT NULL AUTO_INCREMENT, ".
        "runoob_title VARCHAR(100) NOT NULL, ".
        "runoob_author VARCHAR(40) NOT NULL, ".
        "submission_date DATE, ".
        "PRIMARY KEY ( runoob_id ))ENGINE=InnoDB DEFAULT CHARSET=utf8; ";
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('数据表创建失败: ' . mysqli_error($conn));
}
echo "数据表创建成功\n";
mysqli_close($conn);
?>
```

<br />

# 十一. MySQL 删除数据表
### (1) 在命令提示窗口中删除数据表
```sql
mysql> use RUNOOB;
Database changed
mysql> DROP TABLE runoob_tbl;
```

### (2) 使用PHP脚本删除数据表
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
  die('连接失败: ' . mysqli_error($conn));
}
echo '连接成功<br />';
$sql = "DROP TABLE runoob_tbl";
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
  die('数据表删除失败: ' . mysqli_error($conn));
}
echo "数据表删除成功\n";
mysqli_close($conn);
?>
```

> 看了这么多PHP-MySQL代码大体是这样:
> 1. 代码分为三部分: root连接, 选择数据库, 操作数据库. 
> 2. 先把字符串或命令复制给变量, 再把变量带入函数中进行操作.

<br />

# 十二. MySQL 插入数据

### (1) 通过命令提示窗口插入数据
```sql
mysql> use RUNOOB;
Database changed
mysql> INSERT INTO runoob_tbl 
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("学习 PHP", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
mysql> INSERT INTO runoob_tbl
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("学习 MySQL", "菜鸟教程", NOW());
Query OK, 1 rows affected, 1 warnings (0.01 sec)
mysql> INSERT INTO runoob_tbl
    -> (runoob_title, runoob_author, submission_date)
    -> VALUES
    -> ("JAVA 教程", "RUNOOB.COM", '2016-05-06');
Query OK, 1 rows affected (0.00 sec)
```

* 在以上实例中，我们并没有提供 runoob_id 的数据，因为该字段我们在创建表的时候已经设置它为 AUTO_INCREMENT(自动增加) 属性。 所以，该字段会自动递增而不需要我们去设置。
* 实例中 NOW() 是一个 MySQL 函数，该函数返回日期和时间。

#### 读取数据表：
```sql
select * from runoob_tbl;
```

#### 结果:
![img](https://github.com/duckduckk/duckduckk.github.io/blob/master/screenshots/2019-04-10-mysql-table2.png?raw=true)

### (2) 使用PHP脚本插入数据
> 对于含有中文的数据插入，需要添加 `mysqli_query($conn , "set names utf8");` 语句。


```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
  die('连接失败: ' . mysqli_error($conn));
}
echo '连接成功<br />';
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$runoob_title = '学习 Python';
$runoob_author = 'RUNOOB.COM';
$submission_date = '2016-03-06';
 
$sql = "INSERT INTO runoob_tbl ".
        "(runoob_title,runoob_author, submission_date) ".
        "VALUES ".
        "('$runoob_title','$runoob_author','$submission_date')";
 
 
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
  die('无法插入数据: ' . mysqli_error($conn));
}
echo "数据插入成功\n";
mysqli_close($conn);
?>
```

<br />

# 十三. MySQL 查询数据
### (1) 通过命令提示符获取数据
返回数据表 runoob_tbl 的所有记录:
```sql
select * from runoob_tbl;
```

### (2) 使用PHP脚本来获取数据
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'SELECT runoob_id, runoob_title, 
        runoob_author, submission_date
        FROM runoob_tbl';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法读取数据: ' . mysqli_error($conn));
}
echo '<h2>菜鸟教程 mysqli_fetch_array 测试<h2>';
echo '<table border="1"><tr><td>教程 ID</td><td>标题</td><td>作者</td><td>提交日期</td></tr>';
while($row = mysqli_fetch_array($retval, MYSQLI_ASSOC))
{
    echo "<tr><td> {$row['runoob_id']}</td> ".
         "<td>{$row['runoob_title']} </td> ".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['submission_date']} </td> ".
         "</tr>";
}
echo '</table>';
mysqli_close($conn);
?
```

* mysqli_fetch_array() 函数从结果集中取得一行作为关联数组，或数字数组，或二者兼有 返回根据从结果集取得的行生成的数组，如果没有更多行则返回 false。
* PHP mysqli_fetch_array() 函数第二个参数为 MYSQLI_ASSOC， 设置该参数查询结果返回关联数组，可以使用字段名称来作为数组的索引。

#### 结果: (菜鸟教程图) 
![img](http://www.runoob.com/wp-content/uploads/2014/03/9B08EFFD-6326-4C2B-BFCA-171714FC018D.jpg)

### (3) 使用PHP脚本来获取数据 2

PHP 提供了另外一个函数 mysqli_fetch_assoc(), 该函数从结果集中取得一行作为关联数组。 返回根据从结果集取得的行生成的关联数组，如果没有更多行，则返回 false。

主体内容不变, 变的只有下面的部分: 

```php
while($row = mysqli_fetch_assoc($retval))
{
    echo "<tr><td> {$row['runoob_id']}</td> ".
         "<td>{$row['runoob_title']} </td> ".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['submission_date']} </td> ".
         "</tr>";
}
```
### (4) 使用PHP脚本来获取数据 3
也可以使用常量 MYSQLI_NUM 作为 PHP mysqli_fetch_array() 函数的第二个参数，返回数字数组。

> 前面两个返回的是关联数组, 这里返回的是数字数组

```php
while($row = mysqli_fetch_array($retval, MYSQLI_NUM))
{
    echo "<tr><td> {$row[0]}</td> ".
         "<td>{$row[1]} </td> ".
         "<td>{$row[2]} </td> ".
         "<td>{$row[3]} </td> ".
         "</tr>";
}
```

### (5) 内存释放
在我们执行完 SELECT 语句后，释放游标内存是一个很好的习惯。

可以通过 PHP 函数 mysqli_free_result() 来实现内存的释放。
```php
//......
while($row = mysqli_fetch_array($retval, MYSQLI_NUM))
{
    echo "<tr><td> {$row[0]}</td> ".
         "<td>{$row[1]} </td> ".
         "<td>{$row[2]} </td> ".
         "<td>{$row[3]} </td> ".
         "</tr>";
}
echo '</table>';
// 释放内存
mysqli_free_result($retval);
//......
```

<br />

# 十四. MySQL WHERE 子句
* 从 MySQL 表中使用 SQL SELECT 语句来读取数据。
* 如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句中。
* WHERE 子句类似于程序语言中的 if 条件，根据 MySQL 表中的字段值来读取指定的数据。
* WHERE 字句中使用的操作符基本和以前的一样. 只是检测两个值是否相等用`=`. 不等于号用`!=`或`<>`.

### (1) 命令提示窗口
```sql
SELECT * from runoob_tbl WHERE runoob_author='菜鸟教程';
```
![img](https://github.com/duckduckk/duckduckk.github.io/blob/master/screenshots/2019-04-10-mysql-table3.png?raw=true)


MySQL 的 WHERE 子句的字符串比较是不区分大小写的。 可以使用 BINARY 关键字来设定 WHERE 子句的字符串比较区分大小写.
```sql
mysql> SELECT * from runoob_tbl WHERE BINARY runoob_author='runoob.com';
Empty set (0.01 sec)
 
mysql> SELECT * from runoob_tbl WHERE BINARY runoob_author='RUNOOB.COM';
```

### (2) 使用PHP脚本读取数据
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
// 读取 runoob_author 为 RUNOOB.COM 的数据
$sql = 'SELECT runoob_id, runoob_title, 
        runoob_author, submission_date
        FROM runoob_tbl
        WHERE runoob_author="RUNOOB.COM"';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法读取数据: ' . mysqli_error($conn));
}
echo '<h2>菜鸟教程 MySQL WHERE 子句测试<h2>';
echo '<table border="1"><tr><td>教程 ID</td><td>标题</td><td>作者</td><td>提交日期</td></tr>';
while($row = mysqli_fetch_array($retval, MYSQL_ASSOC))
{
    echo "<tr><td> {$row['runoob_id']}</td> ".
         "<td>{$row['runoob_title']} </td> ".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['submission_date']} </td> ".
         "</tr>";
}
echo '</table>';
// 释放内存
mysqli_free_result($retval);
mysqli_close($conn);
?>
```

<br />

# 十五. MySQL UPDATE 查询
如果我们需要修改或更新 MySQL 中的数据，则可以使用 SQL UPDATE 命令来操作。.

### (1) 命令提示窗口
初始状态: 

![img](https://github.com/duckduckk/duckduckk.github.io/blob/master/screenshots/2019-04-10-mysql-table2.png?raw=true)

```sql
mysql> UPDATE runoob_tbl SET runoob_title='学习 C++' WHERE runoob_id=3;
Query OK, 1 rows affected (0.01 sec)
```

修改后:


![img](https://github.com/duckduckk/duckduckk.github.io/blob/master/screenshots/2019-04-10-mysql-table4.png?raw=true)

### (2) 使用PHP脚本更新数据
> 不使用 WHERE 子句将数据表的全部数据进行更新，所以要慎重。

```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'UPDATE runoob_tbl
        SET runoob_title="学习 Python"
        WHERE runoob_id=3';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法更新数据: ' . mysqli_error($conn));
}
echo '数据更新成功！';
mysqli_close($conn);
?>
```

<br />

# 十六. MySQL DELETE 语句

### (1) 从命令行中删除数据
> 如果没有指定 WHERE 子句，MySQL 表中的所有记录将被删除


```sql
mysql> use RUNOOB;
Database changed
mysql> DELETE FROM runoob_tbl WHERE runoob_id=3;
Query OK, 1 row affected (0.23 sec)
```

### (2) 使用 PHP 脚本删除数据
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'DELETE FROM runoob_tbl
        WHERE runoob_id=3';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法删除数据: ' . mysqli_error($conn));
}
echo '数据删除成功！';
mysqli_close($conn);
?>
```

<br />

# 十七. MySQL LIKE 子句
* WHERE 子句中可以使用等号 = 来设定获取数据的条件，如 `runoob_author = 'RUNOOB.COM'`。
* 但是有时候我们需要获取 runoob_author 字段含有 "COM" 字符的所有记录，这时我们就需要在 WHERE 子句中使用 SQL LIKE 子句。
* SQL LIKE 子句中使用百分号 `%`字符来表示任意字符，类似于UNIX或正则表达式中的星号 `*`。
* 如果没有使用百分号 `%`, LIKE 子句与等号 `=` 的效果是一样的。

### (1) 在命令提示符中使用 LIKE 子句
在 runoob_tbl 表中获取 runoob_author 字段中以 COM 为结尾的的所有记录:
```sql
mysql> use RUNOOB;
Database changed
mysql> SELECT * from runoob_tbl  WHERE runoob_author LIKE '%COM';
```

### (2) 在PHP脚本中使用 LIKE 子句
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'SELECT runoob_id, runoob_title, 
        runoob_author, submission_date
        FROM runoob_tbl
        WHERE runoob_author LIKE "%COM"';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法读取数据: ' . mysqli_error($conn));
}
echo '<h2>菜鸟教程 mysqli_fetch_array 测试<h2>';
echo '<table border="1"><tr><td>教程 ID</td><td>标题</td><td>作者</td><td>提交日期</td></tr>';
while($row = mysqli_fetch_array($retval, MYSQLI_ASSOC))
{
    echo "<tr><td> {$row['runoob_id']}</td> ".
         "<td>{$row['runoob_title']} </td> ".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['submission_date']} </td> ".
         "</tr>";
}
echo '</table>';
mysqli_close($conn);
?>
```

<br />

# 十八. MySQL UNION 操作符
* MySQL UNION 操作符用于连接两个以上的 SELECT 语句的结果组合到一个结果集合中。
* 多个 SELECT 语句会删除重复的数据。

### (1) SQL UNION 实例
列出两个表中所有的country的值 (重复的数据会替代掉, 相同的数据只会出现一次) :
```sql
SELECT country FROM Websites
UNION
SELECT country FROM apps
ORDER BY country;
```

### (2) SQL UNION ALL 实例
用 UNION ALL 从 "Websites" 和 "apps" 表中选取所有的country（重复的值不会被替换掉）：
> 注意 UNION 和 UNION ALL 的区别


```sql
SELECT country FROM Websites
UNION ALL
SELECT country FROM apps
ORDER BY country;
```

### (3) 带有 WHERE 的 SQL UNION ALL
列出两个表中country为CN的 country, name,app_name的值:

```sql
SELECT country, name FROM Websites
WHERE country='CN'
UNION ALL
SELECT country, app_name FROM apps
WHERE country='CN'
ORDER BY country;
```

<br />

# 十九. MySQL 排序
* MySQL使用SQL SELECT 语句来排序
* 使用 ORDER BY 字句来对读取的数据进行排序, 并返回结果
*  SQL 语句中, asc是指定列按升序排列，desc则是指定列按降序排列

### (1) 在命令提示符中使用 ORDER BY 子句
读取runoob_tbl表中的所有数据, 并按照其中某一项 (submission_date)来升序排列:
```sql
mysql> use RUNOOB;
Database changed
mysql> SELECT * from runoob_tbl ORDER BY submission_date ASC;
```

降序排列:
```sql
mysql> SELECT * from runoob_tbl ORDER BY submission_date DESC;
```

### (2) 在 PHP 脚本中使用 ORDER BY 子句
使用PHP函数的 mysqli_query() 及相同的 SQL SELECT 带上 ORDER BY 子句的命令来获取数据。
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'SELECT runoob_id, runoob_title, 
        runoob_author, submission_date
        FROM runoob_tbl
        ORDER BY  submission_date ASC';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法读取数据: ' . mysqli_error($conn));
}
echo '<h2>菜鸟教程 MySQL ORDER BY 测试<h2>';
echo '<table border="1"><tr><td>教程 ID</td><td>标题</td><td>作者</td><td>提交日期</td></tr>';
while($row = mysqli_fetch_array($retval, MYSQL_ASSOC))
{
    echo "<tr><td> {$row['runoob_id']}</td> ".
         "<td>{$row['runoob_title']} </td> ".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['submission_date']} </td> ".
         "</tr>";
}
echo '</table>';
mysqli_close($conn);
?>
```

<br />

# 二十. MySQL GROUP BY 语句
* GROUP BY 语句根据一个或多个列对结果集进行分组。
* 在分组的列上可以使用 COUNT, SUM, AVG,等函数。

### (1) 实例演示
初始状态:
```sql
mysql> set names utf8;
mysql> SELECT * FROM employee_tbl;
```
```sql
+----+--------+---------------------+--------+
| id | name   | date                | singin |
+----+--------+---------------------+--------+
|  1 | 小明 | 2016-04-22 15:25:33 |      1 |
|  2 | 小王 | 2016-04-20 15:25:47 |      3 |
|  3 | 小丽 | 2016-04-19 15:26:02 |      2 |
|  4 | 小王 | 2016-04-07 15:26:14 |      4 |
|  5 | 小明 | 2016-04-11 15:26:40 |      4 |
|  6 | 小明 | 2016-04-04 15:26:54 |      2 |
+----+--------+---------------------+--------+
6 rows in set (0.00 sec)
```
使用 GROUP BY 语句 将数据表按名字进行分组，并统计每个人有多少条记录：
```sql
mysql> SELECT name, COUNT(*) FROM   employee_tbl GROUP BY name;
```
```sql

+--------+----------+
| name   | COUNT(*) |
+--------+----------+
| 小丽 |        1 |
| 小明 |        3 |
| 小王 |        2 |
+--------+----------+
3 rows in set (0.01 sec)
```

### (2) 使用 WITH ROLLUP
WITH ROLLUP 可以实现在分组统计数据基础上再进行相同的统计（SUM,AVG,COUNT…）

例如我们将以上的数据表按名字进行分组，再统计每个人登录的次数：
```sql
mysql> SELECT name, SUM(singin) as singin_count FROM  employee_tbl GROUP BY name WITH ROLLUP;
```
```sql
+--------+--------------+
| name   | singin_count |
+--------+--------------+
| 小丽 |            2 |
| 小明 |            7 |
| 小王 |            7 |
| NULL   |           16 |
+--------+--------------+
4 rows in set (0.00 sec)
```
* 其中记录 NULL 表示所有人的登录次数。
* `SUM(singin) as singin_count`的意思是讲`singin`求和 成`singin_count`
* 区别: (1) 只是统计了"记录条数"(一个记录条数里有多个签到次数), 而 (2) 将"记录条数"再求和成另一个数据(总的签到次数)


### (3) coalesce 
我们可以使用 coalesce 来设置一个可以取代 NUll 的名称

```sql
select coalesce(a,b,c);
```
参数说明：如果`a==null`,则选择b；如果`b==null`,则选择c；如果`a!=null`,则选择a；如果a b c 都为null ，则返回为null（没意义）

```sql
mysql> SELECT coalesce(name, '总数'), SUM(singin) as singin_count FROM  employee_tbl GROUP BY name WITH ROLLUP;
```
```sql
+--------------------------+--------------+
| coalesce(name, '总数') | singin_count |
+--------------------------+--------------+
| 小丽                   |            2 |
| 小明                   |            7 |
| 小王                   |            7 |
| 总数                   |           16 |
+--------------------------+--------------+
4 rows in set (0.01 sec)
```
> "NULL" 变成了 "总数"

<br />

# 二十一. Mysql 连接的使用
使用 JOIN 在两个或多个表中查询数据

JOIN 按照功能大致分为如下三类：
* INNER JOIN（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
* LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。
* RIGHT JOIN（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。

### (1) 在命令提示符中使用 INNER JOIN
```sql
mysql> SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a INNER JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
```

```sql
+-------------+-----------------+----------------+
| a.runoob_id | a.runoob_author | b.runoob_count |
+-------------+-----------------+----------------+
| 1           | 菜鸟教程    | 10             |
| 2           | 菜鸟教程    | 10             |
| 3           | RUNOOB.COM      | 20             |
| 4           | RUNOOB.COM      | 20             |
+-------------+-----------------+----------------+
4 rows in set (0.00 sec)
```

* `SELECT a.runoob_id, a.runoob_author, b.runoob_count`为 "结果表" 的表头
* `ROM runoob_tbl a INNER JOIN tcount_tbl b` a对应runoob_tbl表,b对应tcount_tbl表.
* `ON a.runoob_author = b.runoob_author;` 当a.runoob_author＝b.runoob_author时，执行操作

#### 以上 SQL 语句等价于：

```sql
mysql> SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a, tcount_tbl b WHERE a.runoob_author = b.runoob_author;
```

### (2) MySQL LEFT JOIN
MySQL left join 与 join 有所不同。 MySQL LEFT JOIN 会读取左边数据表的全部数据，即便右边表无对应数据。

```sql
mysql> SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a LEFT JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
```

### (3) MySQL RIGHT JOIN
MySQL RIGHT JOIN 会读取右边数据表的全部数据，即便左边边表无对应数据。
```sql
mysql> SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a RIGHT JOIN tcount_tbl b ON a.runoob_author = b.runoob_author;
```

### (4) 在 PHP 脚本中使用 JOIN
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
$sql = 'SELECT a.runoob_id, a.runoob_author, b.runoob_count FROM runoob_tbl a INNER JOIN tcount_tbl b ON a.runoob_author = b.runoob_author';
 
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法读取数据: ' . mysqli_error($conn));
}
echo '<h2>菜鸟教程 MySQL JOIN 测试<h2>';
echo '<table border="1"><tr><td>教程 ID</td><td>作者</td><td>登陆次数</td></tr>';
while($row = mysqli_fetch_array($retval, MYSQL_ASSOC))
{
    echo "<tr><td> {$row['runoob_id']}</td> ".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['runoob_count']} </td> ".
         "</tr>";
}
echo '</table>';
mysqli_close($conn);
?>
```

<br />

# 二十二．　MySQL NULL 值处理
MySQL 使用 SQL SELECT 命令及 WHERE 子句来读取数据表中的数据,但是当提供的查询条件字段为 NULL 时，该命令可能就无法正常工作。

* 关于 NULL 的条件比较运算是比较特殊的。你不能使用 = NULL 或 != NULL 在列中查找 NULL 值 。
* 在 MySQL 中，NULL 值与任何其它值的比较（即使是 NULL）永远返回 false，即 NULL = NULL 返回false 。
* MySQL 中处理 NULL 使用 IS NULL 和 IS NOT NULL 运算符。

> 也就是说如果表中有数值为NULL, 如果你想找到这个NULL, 不能用=NULL或者!= NULL来找, 只能用IS NULL 或者 IS NOT NULL来查找

```sql
mysql> SELECT * FROM runoob_test_tbl WHERE runoob_count IS NULL;
```
```sql
mysql> SELECT * from runoob_test_tbl WHERE runoob_count IS NOT NULL;
```

### (1) 使用 PHP 脚本处理 NULL 值
> isset — 检测变量是否已设置并且非 NULL, 则下面代码中的`isset($runoob_count )`为检测runoob_count是否为空



```sql
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn , "set names utf8");
 
if( isset($runoob_count ))
{
   $sql = "SELECT runoob_author, runoob_count
           FROM  runoob_test_tbl
           WHERE runoob_count = $runoob_count";
}
else
{
   $sql = "SELECT runoob_author, runoob_count
           FROM  runoob_test_tbl
           WHERE runoob_count IS NULL";
}
mysqli_select_db( $conn, 'RUNOOB' );
$retval = mysqli_query( $conn, $sql );
if(! $retval )
{
    die('无法读取数据: ' . mysqli_error($conn));
}
echo '<h2>菜鸟教程 IS NULL 测试<h2>';
echo '<table border="1"><tr><td>作者</td><td>登陆次数</td></tr>';
while($row = mysqli_fetch_array($retval, MYSQL_ASSOC))
{
    echo "<tr>".
         "<td>{$row['runoob_author']} </td> ".
         "<td>{$row['runoob_count']} </td> ".
         "</tr>";
}
echo '</table>';
mysqli_close($conn);
?>
```

<br />

# 二十三. MySQL 正则表达式
* MySQL可以通过 LIKE ...% 来进行模糊匹配。
* MySQL 同样也支持其他正则表达式的匹配， MySQL中使用 REGEXP 操作符来进行正则表达式匹配

可应用于REGEXP 操作符中的正则模式比较多, 具体用的时候再查

### (1) 实例
查找name字段中以'st'为开头的所有数据：
```sql
mysql> SELECT name FROM person_tbl WHERE name REGEXP '^st';
```
查找name字段中以'ok'为结尾的所有数据：
```sql
mysql> SELECT name FROM person_tbl WHERE name REGEXP 'ok$';
```
查找name字段中包含'mar'字符串的所有数据：
```sql
mysql> SELECT name FROM person_tbl WHERE name REGEXP 'mar';
```
查找name字段中以元音字符开头或以'ok'字符串结尾的所有数据：
```sql
mysql> SELECT name FROM person_tbl WHERE name REGEXP '^[aeiou]|ok$';
```

<br />

# 二十四．MySQL 事务
MySQL 事务主要用于处理操作量大，复杂度高的数据。比如说，在人员管理系统中，你删除一个人员，你即需要删除人员的基本资料，也要删除和该人员相关的信息，如信箱，文章等等，这样，这些数据库操作语句就构成一个事务．

* 在 MySQL 中只有使用了 Innodb 数据库引擎的数据库或表才支持事务。
* 事务处理可以用来维护数据库的完整性，保证成批的 SQL 语句要么全部执行，要么全部不执行。
* 事务用来管理 insert,update,delete 语句

### (1) MYSQL 事务处理主要有两种方法：
1. 用 BEGIN, ROLLBACK, COMMIT来实现
* BEGIN 开始一个事务
* ROLLBACK 事务回滚
* COMMIT 事务确认

2. 直接用 SET 来改变 MySQL 的自动提交模式:
* SET AUTOCOMMIT=0 禁止自动提交
* SET AUTOCOMMIT=1 开启自动提交

> 教程上说的好复杂，其实直接看代码就能懂．知道意思就行了

```sql
mysql> use RUNOOB;
Database changed
mysql> CREATE TABLE runoob_transaction_test( id int(5)) engine=innodb;  # 创建数据表
Query OK, 0 rows affected (0.04 sec)
 
mysql> select * from runoob_transaction_test;
Empty set (0.01 sec)
 
mysql> begin;  # 开始事务
Query OK, 0 rows affected (0.00 sec)
 
mysql> insert into runoob_transaction_test value(5);
Query OK, 1 rows affected (0.01 sec)
 
mysql> insert into runoob_transaction_test value(6);
Query OK, 1 rows affected (0.00 sec)
 
mysql> commit; # 提交事务
Query OK, 0 rows affected (0.01 sec)
 
mysql>  select * from runoob_transaction_test;
+------+
| id   |
+------+
| 5    |
| 6    |
+------+
2 rows in set (0.01 sec)
 
mysql> begin;    # 开始事务
Query OK, 0 rows affected (0.00 sec)
 
mysql>  insert into runoob_transaction_test values(7);
Query OK, 1 rows affected (0.00 sec)
 
mysql> rollback;   # 回滚
Query OK, 0 rows affected (0.00 sec)
 
mysql>   select * from runoob_transaction_test;   # 因为回滚所以数据没有插入
+------+
| id   |
+------+
| 5    |
| 6    |
+------+
2 rows in set (0.01 sec)
 
mysql>
```

### (2) PHP中使用事务实例
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
mysqli_query($conn, "set names utf8");
mysqli_select_db( $conn, 'RUNOOB' );
mysqli_query($conn, "SET AUTOCOMMIT=0"); // 设置为不自动提交，因为MYSQL默认立即执行
mysqli_begin_transaction($conn);            // 开始事务定义
 
if(!mysqli_query($conn, "insert into runoob_transaction_test (id) values(8)"))
{
    mysqli_query($conn, "ROLLBACK");     // 判断当执行失败时回滚
}
 
if(!mysqli_query($conn, "insert into runoob_transaction_test (id) values(9)"))
{
    mysqli_query($conn, "ROLLBACK");      // 判断执行失败时回滚
}
mysqli_commit($conn);            //执行事务
mysqli_close($conn);
?>
```

> 个人觉得所谓＂事务＂, 就是有些命令必须一起执行, 不允许中间出错. 所以我们在写命令时, 必须设定, 如果中间步骤出错, 就立即回滚. 且, 设定不立即提交(MySQL默认立即提交), 所有命令成功执行后再提交(commit)


<br />

# 二十五. MySQL ALTER命令
### (1) 删除，添加或修改表字段
如下命令使用了 ALTER 命令及 DROP 子句来删除以上创建表的 i 字段：
```sql
mysql> ALTER TABLE testalter_tbl  DROP i;
```
> 如果数据表中只剩余一个字段则无法使用DROP来删除字段。

MySQL 中使用 ADD 子句来向数据表中添加列，如下实例在表 testalter_tbl 中添加 i 字段，并定义数据类型:
```sql
mysql> ALTER TABLE testalter_tbl ADD i INT;
```
执行以上命令后，i 字段会自动添加到数据表字段的末尾。

查看表信息: 
```sql
mysql> SHOW COLUMNS FROM testalter_tbl;
```

如果需要指定新增字段的位置，可以使用MySQL提供的关键字 FIRST (设定位第一列)， AFTER 字段名（设定位于某个字段之后）:
```sql
ALTER TABLE testalter_tbl DROP i;
ALTER TABLE testalter_tbl ADD i INT FIRST;
ALTER TABLE testalter_tbl DROP i;
ALTER TABLE testalter_tbl ADD i INT AFTER c;
```

### (2) 修改字段类型及名称
如果需要修改字段类型及名称, 可以在ALTER命令中使用 MODIFY 或 CHANGE 子句 

把字段 c 的类型从 CHAR(1) 改为 CHAR(10)
```sql
mysql> ALTER TABLE testalter_tbl MODIFY c CHAR(10);
```
使用 CHANGE 子句:
```sql
mysql> ALTER TABLE testalter_tbl CHANGE i j BIGINT;
mysql> ALTER TABLE testalter_tbl CHANGE j j INT;
```

### (3) ALTER TABLE 对 Null 值和默认值的影响
* 当修改字段时，可以指定是否包含值或者是否设置默认值。
* 如果不设置默认值，MySQL会自动设置该字段默认为 NULL。


指定字段 j 为 NOT NULL 且默认值为100 :
```sql
mysql> ALTER TABLE testalter_tbl 
    -> MODIFY j BIGINT NOT NULL DEFAULT 100;
```

### (4) 修改字段默认值
#### 修改字段的默认值:
```sql
mysql> ALTER TABLE testalter_tbl ALTER i SET DEFAULT 1000;
```
#### 删除字段的默认值：
```sql
mysql> ALTER TABLE testalter_tbl ALTER i DROP DEFAULT;
```
#### 修改数据表类型
> 查看数据表类型可以使用 `SHOW TABLE STATUS` 语句。

```sql
mysql> ALTER TABLE testalter_tbl ENGINE = MYISAM;
mysql>  SHOW TABLE STATUS LIKE 'testalter_tbl'\G    //查看表类型
```

#### 修改表名
```sql
mysql> ALTER TABLE testalter_tbl RENAME TO alter_tbl;
```

<br />

# 二十六. MySQL 索引
> 你一个例子都不给我, 我怎么看得懂.........(小声bb)
> 过两天也要顺便看 课上的MySQL(要考试了), 到时候再看吧, 今晚想早点看完, 然后去浪...

[菜鸟教程MySQL索引](http://www.runoob.com/mysql/mysql-index.html)

<br />

# 二十七. MySQL 临时表

* MySQL 临时表在我们需要保存一些临时数据时是非常有用的。临时表只在当前连接可见，当关闭连接时，Mysql会自动删除表并释放所有空间。
* MySQL临时表只在当前连接可见，如果你使用PHP脚本来创建MySQL临时表，那每当PHP脚本执行完成后，该临时表也会自动销毁。
* 如果你使用了其他MySQL客户端程序连接MySQL数据库服务器来创建临时表，那么只有在关闭客户端程序时才会销毁临时表，当然你也可以手动销毁。

### (1) 实例
```sql
mysql> CREATE TEMPORARY TABLE SalesSummary (
    -> product_name VARCHAR(50) NOT NULL
    -> , total_sales DECIMAL(12,2) NOT NULL DEFAULT 0.00
    -> , avg_unit_price DECIMAL(7,2) NOT NULL DEFAULT 0.00
    -> , total_units_sold INT UNSIGNED NOT NULL DEFAULT 0
);
Query OK, 0 rows affected (0.00 sec)

mysql> INSERT INTO SalesSummary
    -> (product_name, total_sales, avg_unit_price, total_units_sold)
    -> VALUES
    -> ('cucumber', 100.25, 90, 2);

mysql> SELECT * FROM SalesSummary;
+--------------+-------------+----------------+------------------+
| product_name | total_sales | avg_unit_price | total_units_sold |
+--------------+-------------+----------------+------------------+
| cucumber     |      100.25 |          90.00 |                2 |
+--------------+-------------+----------------+------------------+
1 row in set (0.00 sec)
```

### (2) 删除MySQL 临时表
* 默认情况下，断开与数据库的连接后，临时表就会自动被销毁
* 也可以在当前MySQL会话使用 DROP TABLE 命令来手动删除临时表
```sql
mysql> DROP TABLE SalesSummary;
mysql>  SELECT * FROM SalesSummary;
ERROR 1146: Table 'RUNOOB.SalesSummary' doesn't exist
```

<br />

# 二十八. MySQL 复制表

步骤如下：
* 使用 SHOW CREATE TABLE 命令获取创建数据表(CREATE TABLE) 语句，该语句包含了原数据表的结构，索引等。
* 修改SQL语句的数据表名，并执行SQL语句，通过以上命令 将完全的复制数据表结构。
* 如果你想复制表的内容，你就可以使用 INSERT INTO ... SELECT 语句来实现。

即: 
* 获取原表的结构
* 创建新表的结构
* 复制表的内容(数据)

### 步骤一：

```sql
mysql> SHOW CREATE TABLE runoob_tbl \G;
*************************** 1. row ***************************
       Table: runoob_tbl
Create Table: CREATE TABLE `runoob_tbl` (
  `runoob_id` int(11) NOT NULL auto_increment,
  `runoob_title` varchar(100) NOT NULL default '',
  `runoob_author` varchar(40) NOT NULL default '',
  `submission_date` date default NULL,
  PRIMARY KEY  (`runoob_id`),
  UNIQUE KEY `AUTHOR_INDEX` (`runoob_author`)
) ENGINE=InnoDB 
1 row in set (0.00 sec)

ERROR:
No query specified
```
### 步骤二：

```sql
mysql> CREATE TABLE `clone_tbl` (
  -> `runoob_id` int(11) NOT NULL auto_increment,
  -> `runoob_title` varchar(100) NOT NULL default '',
  -> `runoob_author` varchar(40) NOT NULL default '',
  -> `submission_date` date default NULL,
  -> PRIMARY KEY  (`runoob_id`),
  -> UNIQUE KEY `AUTHOR_INDEX` (`runoob_author`)
-> ) ENGINE=InnoDB;
Query OK, 0 rows affected (1.80 sec)
```
### 步骤三：

```sql
mysql> INSERT INTO clone_tbl (runoob_id,
    ->                        runoob_title,
    ->                        runoob_author,
    ->                        submission_date)
    -> SELECT runoob_id,runoob_title,
    ->        runoob_author,submission_date
    -> FROM runoob_tbl;
Query OK, 3 rows affected (0.07 sec)
Records: 3  Duplicates: 0  Warnings: 0
```
执行以上步骤后，你将完整的复制表，包括表结构及表数据。

<br />

# 二十九. MySQL 元数据
MySQL有以下三种信息：
* 查询结果信息： SELECT, UPDATE 或 DELETE语句影响的记录数。
* 数据库和数据表的信息： 包含了数据库及数据表的结构信息。
* MySQL服务器信息： 包含了数据库服务器的当前状态，版本号等。

在MySQL的命令提示符中，可以很容易的获取以上服务器信息。 但如果使用Perl或PHP等脚本语言，就需要调用特定的接口函数来获取。 
> 意思是, 通过MySQL命令行可以很轻松获取以上三种信息, 但是现在要通过Perl和PHP来获取....Perl就先不看了....吧

### (1) 获取查询语句影响的记录数
在PHP中，可以使用 mysqli_affected_rows( ) 函数来获取查询语句影响的记录数。
```php
$result_id = mysqli_query ($conn_id, $query);
# 如果查询失败返回 
$count = ($result_id ? mysqli_affected_rows ($conn_id) : 0);
print ("$count 条数据被影响\n");
```

### (2) 数据库和数据表列表
以下实例输出 MySQL 服务器上的所有数据库：
```php
<?php
$dbhost = 'localhost:3306';  // mysql服务器主机地址
$dbuser = 'root';            // mysql用户名
$dbpass = '123456';          // mysql用户名密码
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('连接失败: ' . mysqli_error($conn));
}
// 设置编码，防止中文乱码
$db_list = mysqli_query($conn, 'SHOW DATABASES');
while ($db = mysqli_fetch_object($db_list))
{
  echo $db->Database . "<br />";
}
mysqli_close($conn);
?>
```

<br />

# 三十. MySQL 序列使用
MySQL 序列是一组整数：1, 2, 3, ...，由于一张数据表只能有一个字段自增主键， 如果想实现其他字段也实现自动增加，就可以使用MySQL序列来实现

### (1) 使用 AUTO_INCREMENT
```sql
mysql> CREATE TABLE insect
    -> (
    -> id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    -> PRIMARY KEY (id),
    -> name VARCHAR(30) NOT NULL, # type of insect
    -> date DATE NOT NULL, # date collected
    -> origin VARCHAR(30) NOT NULL # where collected
);
Query OK, 0 rows affected (0.02 sec)
```

### (2) 获取AUTO_INCREMENT值
* PHP 通过 mysql_insert_id ()函数来获取执行的插入SQL语句中 AUTO_INCREMENT列的值
* 获取最后的插入表中的自增列的值
> 就是如果表中id为113的话, 现在获取到113这个值.


```php
mysql_query ("INSERT INTO insect (name,date,origin)
VALUES('moth','2001-09-14','windowsill')", $conn_id);
$seq = mysql_insert_id ($conn_id);
```

### (3) 重置序列
如果希望对剩下数据的AUTO_INCREMENT列进行重新排列，那么可以通过删除自增的列，然后重新添加来实现。
```sql
mysql> ALTER TABLE insect DROP id;
mysql> ALTER TABLE insect
    -> ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT FIRST,
    -> ADD PRIMARY KEY (id);
```

### (4) 设置序列的开始值
一般情况下序列的开始值为1，但如果你需要指定一个开始值100，那我们可以通过以下语句来实现：
```sql
mysql> CREATE TABLE insect
    -> (
    -> id INT UNSIGNED NOT NULL AUTO_INCREMENT,
    -> PRIMARY KEY (id),
    -> name VARCHAR(30) NOT NULL, 
    -> date DATE NOT NULL,
    -> origin VARCHAR(30) NOT NULL
)engine=innodb auto_increment=100 charset=utf8;
```
或者你也可以在表创建成功后，通过以下语句来实现：
```sql
mysql> ALTER TABLE t AUTO_INCREMENT = 100;
```

<br />

# 三十一. MySQL 处理重复数据
### (1) 防止表中出现重复数据
可以在 MySQL 数据表中设置指定的字段为 PRIMARY KEY（主键） 或者 UNIQUE（唯一） 索引来保证数据的唯一性。


可以设置双主键模式来设置数据的唯一性， 如果你设置了双主键，那么那个键的默认值不能为 NULL，可设置为 NOT NULL.
```sql
CREATE TABLE person_tbl
(
   first_name CHAR(20) NOT NULL,
   last_name CHAR(20) NOT NULL,
   sex CHAR(10),
   PRIMARY KEY (last_name, first_name)
);
```

* INSERT IGNORE INTO 
    INSERT IGNORE 会忽略数据库中已经存在的数据，如果数据库没有数据，就插入新的数据，如果有数据的话就跳过这条数据。这样就可以保留数据库中已经存在数据，达到在间隙中插入数据的目的。当插入数据时，在设置了记录的唯一性后，如果插入重复数据，将不返回错误，只以警告形式返回。
    ```sql
    mysql> INSERT IGNORE INTO person_tbl (last_name, first_name)
        -> VALUES( 'Jay', 'Thomas');
    Query OK, 0 rows affected (0.00 sec)    
    ``` 
* INSERT INTO

* REPLACE INTO 
如果存在 primary 或 unique 相同的记录，则先删除掉。再插入新记录。

#### 另一种设置数据的唯一性方法是添加一个 UNIQUE 索引
```sql
CREATE TABLE person_tbl
(
   first_name CHAR(20) NOT NULL,
   last_name CHAR(20) NOT NULL,
   sex CHAR(10),
   UNIQUE (last_name, first_name)
);
```

### (2) 统计重复数据
统计表中 first_name 和 last_name的重复记录数：
```sql
mysql> SELECT COUNT(*) as repetitions, last_name, first_name
    -> FROM person_tbl
    -> GROUP BY last_name, first_name
    -> HAVING repetitions > 1;
```
HAVING子句设置重复数大于1

### (3) 过滤重复数据
如果需要读取不重复的数据可以在 SELECT 语句中使用 DISTINCT 关键字来过滤重复数据。
```sql
mysql> SELECT DISTINCT last_name, first_name
    -> FROM person_tbl;
```
也可以使用 GROUP BY 来读取数据表中不重复的数据：
```sql
mysql> SELECT last_name, first_name
    -> FROM person_tbl
    -> GROUP BY (last_name, first_name);
```

### (4) 删除重复数据
```sql
mysql> CREATE TABLE tmp SELECT last_name, first_name, sex FROM person_tbl  GROUP BY (last_name, first_name, sex);
mysql> DROP TABLE person_tbl;
mysql> ALTER TABLE tmp RENAME TO person_tbl;
```
当然也可以在数据表中添加 INDEX（索引） 和 PRIMAY KEY（主键）这种简单的方法来删除表中的重复记录:
```sql
mysql> ALTER IGNORE TABLE person_tbl
    -> ADD PRIMARY KEY (last_name, first_name);
```

<br />

# 三十二. MySQL 及 SQL 注入
所谓SQL注入，就是通过把SQL命令插入到Web表单递交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令。

> 正则表达式找时间好好看看

防止SQL注入，需要注意以下几个要点：
1. 永远不要信任用户的输入。对用户的输入进行校验，可以通过正则表达式，或限制长度；对单引号和 双"-"进行转换等。
2. 永远不要使用动态拼装sql，可以使用参数化的sql或者直接使用存储过程进行数据查询存取。
3. 永远不要使用管理员权限的数据库连接，为每个应用使用单独的权限有限的数据库连接。
4. 不要把机密信息直接存放，加密或者hash掉密码和敏感的信息。
5. 应用的异常信息应该给出尽可能少的提示，最好使用自定义的错误信息对原始错误信息进行包装
6. sql注入的检测方法一般采取辅助软件或网站平台来检测，软件一般采用sql注入检测工具jsky，网站平台就有亿思网站安全平台检测工具。MDCSOFT SCAN等。采用MDCSOFT-IPS可以有效的防御SQL注入，XSS攻击等。

### (1) 防止SQL注入
* 在脚本语言，如Perl和PHP你可以对用户输入的数据进行转义从而来防止SQL注入。
* PHP的MySQL扩展提供了mysqli_real_escape_string()函数来转义特殊的输入字符。
```php
if (get_magic_quotes_gpc()) 
{
  $name = stripslashes($name);
}
$name = mysqli_real_escape_string($conn, $name);
 mysqli_query($conn, "SELECT * FROM users WHERE name='{$name}'");
```

### (2) Like语句中的注入
* like查询时，如果用户输入的值有"_"和"%"，则会出现这种情况：用户本来只是想查询"abcd_"，查询结果中却有"abcd_"、"abcde"、"abcdf"等等；用户要查询"30%"（注：百分之三十）时也会出现问题。
* 在PHP脚本中我们可以使用addcslashes()函数来处理以上情况，如下实例：

```php
$sub = addcslashes(mysqli_real_escape_string($conn, "%something_"), "%_");
// $sub == \%something\_
 mysqli_query($conn, "SELECT * FROM messages WHERE subject LIKE '{$sub}%'");
```
addcslashes() 函数在指定的字符前添加反斜杠。

<br />

# 三十三. MySQL 导出数据

### (1) 使用 SELECT ... INTO OUTFILE 语句导出数据
将数据表 runoob_tbl 数据导出到 /tmp/runoob.txt 文件中:
```sql
mysql> SELECT * FROM runoob_tbl 
    -> INTO OUTFILE '/tmp/runoob.txt';
```
也可以通过命令选项来设置数据输出的指定格式，以下实例为导出 CSV 格式：
```sql
mysql> SELECT * FROM passwd INTO OUTFILE '/tmp/runoob.txt'
    -> FIELDS TERMINATED BY ',' ENCLOSED BY '"'
    -> LINES TERMINATED BY '\r\n';
```
生成一个文件，各值用逗号隔开。这种格式可以被许多程序使用:
```sql
SELECT a,b,a+b INTO OUTFILE '/tmp/result.text'
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n'
FROM test_table;
```

### (2) 导出表作为原始数据
* mysqldump 是 mysql 用于转存储数据库的实用程序。它主要产生一个 SQL 脚本，其中包含从头重新创建数据库所必需的命令 CREATE TABLE INSERT 等。

* 使用 mysqldump 导出数据需要使用 --tab 选项来指定导出文件指定的目录，该目标必须是可写的。

以下实例将数据表 runoob_tbl 导出到 `/tmp` 目录中：
```sql
$ mysqldump -u root -p --no-create-info \
            --tab=/tmp RUNOOB runoob_tbl
password ******
```

### (3) 导出 SQL 格式的数据
导出 SQL 格式的数据到指定文件：
```shell
$ mysqldump -u root -p RUNOOB runoob_tbl > dump.txt
password ******
```
如果需要导出整个数据库的数据：
```shell
$ mysqldump -u root -p RUNOOB > database_dump.txt
password ******
```
如果需要备份所有数据库：
```shell
$ mysqldump -u root -p --all-databases > database_dump.txt
password ******
```

### (4) 将数据表及数据库拷贝至其他主机
如果需要将数据拷贝至其他的 MySQL 服务器上, 可以在 mysqldump 命令中指定数据库名及数据表。

在源主机上执行以下命令，将数据备份至 dump.txt 文件中(如果完整备份数据库，则无需使用特定的表名称):
```sql
$ mysqldump -u root -p database_name table_name > dump.txt
password *****
```


如果需要将备份的数据库导入到MySQL服务器中，可以使用以下命令，使用以下命令需要确认数据库已经创建：
```sql
$ mysql -u root -p database_name < dump.txt
password *****
```
也可以使用以下命令将导出的数据直接导入到远程的服务器上，但请确保两台服务器是相通的，是可以相互访问的  (以下命令中使用了管道来将导出的数据导入到指定的远程主机上) ：
```sql
$ mysqldump -u root -p database_name \
       | mysql -h other-host.com database_name
```

<br />

# 三十四. MySQL 导入数据

### (1) mysql 命令导入
将将备份的整个数据库 runoob.sql 导入
```shell
mysql -uroot -p123456 < runoob.sql
```

### (2) source 命令导入
source 命令导入数据库需要先登录到数库终端：
```sql
mysql> create database abc;      # 创建数据库
mysql> use abc;                  # 使用已创建的数据库 
mysql> set names utf8;           # 设置编码
mysql> source /home/abc/abc.sql  # 导入备份数据库
```

### (3) 使用 LOAD DATA 导入数据
MySQL 中提供了LOAD DATA INFILE语句来插入数据。 以下实例中将从当前目录中读取文件 dump.txt ，将该文件中的数据插入到当前数据库的 mytbl 表中。
```sql
mysql> LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl;
```

* 如果指定LOCAL关键词，则表明从客户主机上按路径读取文件。如果没有指定，则文件在服务器上按路径读取文件。
* 可以明确地在LOAD DATA语句中指出列值的分隔符和行尾标记，但是默认标记是定位符和换行符。
* 两个命令的 FIELDS 和 LINES 子句的语法是一样的。两个子句都是可选的，但是如果两个同时被指定，FIELDS 子句必须出现在 LINES 子句之前。
    ```sql
    mysql> LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl
  -> FIELDS TERMINATED BY ':'
  -> LINES TERMINATED BY '\r\n';
  ```

LOAD DATA 默认情况下是按照数据文件中列的顺序插入数据的，如果数据文件中的列与插入表中的列不一致，则需要指定列的顺序。

如，在数据文件中的列顺序是 a,b,c，但在插入表的列顺序为b,c,a，则数据导入语法如下：
```sql
mysql> LOAD DATA LOCAL INFILE 'dump.txt' 
    -> INTO TABLE mytbl (b, c, a);
```

### (4) 使用 mysqlimport 导入数据
mysqlimport客户端提供了LOAD DATA INFILEQL语句的一个命令行接口。mysqlimport的大多数选项直接对应LOAD DATA INFILE子句。

从文件 dump.txt 中将数据导入到 mytbl 数据表中, 可以使用以下命令：
```shell
$ mysqlimport -u root -p --local database_name dump.txt
password *****
```
mysqlimport命令可以指定选项来设置指定格式,命令语句格式如下：
```shell
$ mysqlimport -u root -p --local --fields-terminated-by=":" \
   --lines-terminated-by="\r\n"  database_name dump.txt
password *****
```
mysqlimport 语句中使用 --columns 选项来设置列的顺序：
```shell
$ mysqlimport -u root -p --local --columns=b,c,a \
    database_name dump.txt
password *****
```

<br />

# 三十五. MySQL 函数
> 太多, 看教程

<br />

# 三十六. MySQL 运算符
> 需要用的时候看教程吧.


MySQL 主要有以下几种运算符：
* 算术运算符
* 比较运算符
* 逻辑运算符
* 位运算符

### (1) 算数运算符
加法实例:
```sql
mysql> select 1+2;
+-----+
| 1+2 |
+-----+
|   3 |
+-----+
```

### (2) 比较运算符
比较结果为真，则返回 1，为假则返回 0，比较结果不确定则返回 NULL。
#### 其中:
安全等于`<=>` :
与 `=` 的区别在于当两个操作码均为 NULL 时，其所得值为 1 而不为 NULL，而当一个操作码为 NULL 时，其所得值为 0而不为 NULL。

### (3) 逻辑运算符
* `NOT` 或 `!`	逻辑非
* `AND`	逻辑与
* `OR`	逻辑或
* `XOR`	逻辑异或

### (4) 位运算符
位运算符是在二进制数上进行计算的运算符。位运算会先将操作数变成二进制数，进行位运算。然后再将计算结果从二进制数变回十进制数。

* `&`	按位与
* `|`	按位或
* `^`	按位异或
* `!`	取反
* `<<`	左移
* `>>`	右移
