---
layout: post
title: "JS Object 实例"
date: 2019-04-08
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> 前几天看完了js的大体内容, 现在看一些实例来巩固一下, 不然就像当初看python一样, 看完就忘了.


[参考w3school-js对象实例](http://www.w3school.com.cn/example/jsrf_examples.asp)

# 一. JavaScript String
### (1) 返回字符串的长度
```html
<script type="text/javascript">

var txt="Hello World!"
document.write(txt.length)

</script>
```
返回:  `12`

### (2) 为字符串添加样式
```js
var txt="Hello World!"

document.write("<p>Big: " + txt.big() + "</p>")
document.write("<p>Small: " + txt.small() + "</p>")
```
返回: `Big: Hello World!` 等

### (3) 返回字符串中指定文本首次出现的位置 - indexOf()方法
```js
var str="Hello world!"
document.write(str.indexOf("Hello") + "<br />")
document.write(str.indexOf("World") + "<br />")
document.write(str.indexOf("world"))
```
返回:
```
0
-1
6
```

### (4) 查找字符串中特定的字符，若找到，则返回该字符 - match() 方法
```js
var str="Hello world!"
document.write(str.match("world") + "<br />")
document.write(str.match("World") + "<br />")
document.write(str.match("worlld") + "<br />")
document.write(str.match("world!"))
```
返回:
```
world
null
null
world!
```

### (5) 替换字符串中的字符 - replace()
```js
var str="Visit Microsoft!"
document.write(str.replace(/Microsoft/,"W3School"))
```
返回: `Visit W3School!`

<br />

# 二. JavaScript Date
### (1) 使用 Date() 方法来返回今天的日期和时间
```js
document.write(Date())
```
返回: `Mon Apr 08 2019 15:53:27 GMT+0800 (中国标准时间)`

### (2) 使用 getTime() 计算从1970年到今天有多少年
```js
var d=new Date(); //新建一个 date 类
document.write("从 1970/01/01 至今已有：" + d.getTime() + " 毫秒。"); //date类的对象 d 调用函数getTime()
```
返回: `从 1970/01/01 至今已有：1554710176270 毫秒。`
> 不是说求年数吗, 为什么代码是返回秒数, 估计这儿弄错了.


### (3) 使用 setFullYear() 设置具体的日期
```js
var d = new Date()
d.setFullYear(1992,10,3)
document.write(d)
```
返回: `Tue Nov 03 1992 15:58:20 GMT+0800 (中国标准时间)`

### (4) 使用 toUTCString() 把当日的日期（根据 UTC）转换为字符串
```js
var d = new Date()
document.write (d.toUTCString())
```
返回一个字符串:  `Mon, 08 Apr 2019 08:01:16 GMT`

### (5) 使用 getDay() 来显示星期，而不仅仅是数字
```js
var d=new Date()
var weekday=new Array(7) //新建一个数组
weekday[0]="星期日"
weekday[1]="星期一"
weekday[2]="星期二"
weekday[3]="星期三"
weekday[4]="星期四"
weekday[5]="星期五"
weekday[6]="星期六"

document.write("今天是" + weekday[d.getDay()])
```
返回: `今天是星期一`

### (6) 显示一个钟表
```html
<head>
<script type="text/javascript">
function startTime()
{
var today=new Date()
var h=today.getHours()
var m=today.getMinutes()
var s=today.getSeconds()
// add a zero in front of numbers<10
m=checkTime(m)
s=checkTime(s)
document.getElementById('txt').innerHTML=h+":"+m+":"+s
t=setTimeout('startTime()',500)  //500毫秒就刷新一次, 即重新输出, 兼顾精度与执行速度
}

function checkTime(i)
{
if (i<10) 
  {i="0" + i}
  return i
}
</script>
</head>

<!--body 加载 500毫秒刷新一次 的函数-->
<body onload="startTime()"> 
<!--输出部分-->
<div id="txt"></div>  
</body>
```
返回: `16:16:12`之类的

<br />

# 三. JavaScript Boolean
```js
<script type="text/javascript">
var b1=new Boolean( 0)
var b2=new Boolean(1)
var b3=new Boolean("")
var b4=new Boolean(null)
var b5=new Boolean(NaN)
var b6=new Boolean("false")

document.write("0 是逻辑的 "+ b1 +"<br />")
document.write("1 是逻辑的 "+ b2 +"<br />")
document.write("空字符串是逻辑的 "+ b3 + "<br />")
document.write("null 是逻辑的 "+ b4+ "<br />")
document.write("NaN 是逻辑的 "+ b5 +"<br />")
document.write("字符串 'false' 是逻辑的 "+ b6 +"<br />")
</script>
```
返回: 
```
0 是逻辑的 false
1 是逻辑的 true
空字符串是逻辑的 false
null 是逻辑的 false
NaN 是逻辑的 false
字符串 'false' 是逻辑的 true
```

<br />

# 四. JavaScript Math
### (1) 使用 round() 对数字进行舍入
```js
document.write(Math.round(0.60) + "<br />")
document.write(Math.round(0.50) + "<br />")
document.write(Math.round(0.49) + "<br />")
document.write(Math.round(-4.40) + "<br />")
document.write(Math.round(-4.60))
```
返回: 
```
1
1
0
-4
-5
```

### (2) 使用 random() 来返回 0 到 1 之间的随机数
```js
document.write(Math.random())
```
返回一个随机数: `0.8373350191134163`

### (3) 使用 max() 来返回两个给定的数中的较大的数
```js
document.write(Math.max(5,7) + "<br />")
```
返回: `7`

### (4) 使用 min() 来返回两个给定的数中的较小的数
```js
document.write(Math.min(7.25,7.30))
```
返回: `7.25`



