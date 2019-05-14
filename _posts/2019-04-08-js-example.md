---
layout: post
title: "JS 实例"
date: 2019-04-08
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> js-example, 看完这一部分就去看 MySQL和 SQLite

[参考w3school](http://www.w3school.com.cn/example/jseg_examples.asp)

# 一. 基础 JavaScript 实例
### (1) 外部 JavaScript
```js
<script src="/js/example_externaljs.js">
</script>
```

<br />

# 二. JavaScript 语句、注释和代码块
> 飘过....


<br />

# 三. JavaScript 变量

<br />

# 四. JavaScript 条件语句 If ... Else

<br />

# 五. JavaScript 消息框
### (1) 警告框
```html
<html>
<head>
<script type="text/javascript">
function disp_alert()
{
alert("我是警告框！！")
}
</script>
</head>
<body>

<input type="button" onclick="disp_alert()" value="显示警告框" />

</body>
</html>
```
### (2) 带有折行的警告框
```js
function disp_alert()
{
alert("再次向您问好！在这里，我们向您演示" + '\n' + "如何向警告框添加折行。")
}
```
> `'\n'`实现折行


### (3) 确认框
```html
<html>
<head>
<script type="text/javascript">
function show_confirm()
{
//该段代码可以弹出一个确认框
var r=confirm("Press a button!");
if (r==true)
  {
  alert("You pressed OK!");
  }
else
  {
  alert("You pressed Cancel!");
  }
}
</script>
</head>
<body>

<input type="button" onclick="show_confirm()" value="Show a confirm box" />

</body>
</html>
```
### (4) 提示框
```html
<html>
<head>
<script type="text/javascript">
function disp_prompt()
  {
    //Bill Gates会出现在输入框中, 起提示作用
  var name=prompt("请输入您的名字","Bill Gates")
  if (name!=null && name!="")
    {
    document.write("你好！" + name + " 今天过得怎么样？")
    }
  }
</script>
</head>
<body>

<input type="button" onclick="disp_prompt()" value="显示提示框" />

</body>
</html>
```

<br />

# 六. JavaScript 函数
### (1) 带有参数的函数
```js
function myfunction(txt)
{
alert(txt)
}
```
```html
<form>
<input type="button" onclick="myfunction('您好！')" value="调用函数">
</form>
```
警告框会输出 `您好`

<br />

# 七. JavaScript 循环
### (1) 循环产生 HTML 标题
```js
for (i = 1; i <= 6; i++)
{
document.write("<h" + i + ">这是标题 " + i)
document.write("</h" + i + ">")
}
```
就能依次产生标题1,2,3....


### (2) 使用 For...In 声明来遍历数组内的元素
```js
var x
var mycars = new Array()
mycars[0] = "宝马"
mycars[1] = "奔驰"
mycars[2] = "宾利"

for (x in mycars)
{
document.write(mycars[x] + "<br />")
}
```

<br />

# 八. JavaScript 错误处理
### (1) try...catch 语句
```js
function message()
{
    //尝试操作
try
   {
   adddlert("Welcome guest!")
   }
   //如果错误,则抛出报错
catch(err)
   {
   txt="本页中存在错误。\n\n"
   txt+="错误描述：" + err.description + "\n\n"
   txt+="点击“确定”继续。\n\n"
   alert(txt)
   }
}
```
### (2) 带有确认框的 try...catch 语句
```js
function message()
{
try
   {
   adddlert("Welcome guest!")
   }
catch(err)
   {
     txt="本页中存在错误。\n\n"
     txt+="点击“确定”继续查看本页，\n"
     txt+="点击“取消”返回首页。\n\n"
     // 先执行confim(txt),即弹出确认框,再判断
     if(!confirm(txt))
         {
             //如果判断错误,则转到某页面
         document.location.href="/index.html"
         }
   }
}
```

### (3) throw 声明
```js
//prompt()里面的逗号","表示输入框中没有提示内容
var x=prompt("请输入 0 至 10 之间的数：","")
try
{ 
if(x>10) 
  throw "Err1" 
else if(x<0)
  throw "Err2"
else if(isNaN(x))
  throw "Err3"
} 
catch(er)
{
if(er=="Err1") 
  alert("错误！该值太大！")
if(er == "Err2") 
  alert("错误！该值太小！") 
if(er == "Err3") 
  alert("错误！该值不是数字！") 
}
```
> prompt() 方法用于显示可提示用户进行输入的对话框。个人理解为弹出一个有提示内容输入框

### (4) onerror 事件
```html
<html>
<head>
<script type="text/javascript">
//注意这儿
onerror=handleErr
var txt=""
//注意这儿
function handleErr(msg,url,l)
{
txt="本页中存在错误。\n\n"
txt+="错误：" + msg + "\n"
txt+="URL: " + url + "\n"
txt+="行：" + l + "\n\n"
txt+="点击“确定”继续。\n\n"
alert(txt)
return true
}
//注意这儿
function message()
{
adddlert("Welcome guest!")
}
</script>
</head>

<body>
<input type="button" value="查看消息" onclick="message()" />
</body>

</html>
```
> onerror 事件 有关于图片的报错类. 图片的报错我能看懂. 而这儿的例子我有点懵逼.

 注意代码中我注释的三处"注意", 以下是个人理解
* 将报错函数的值赋值给onerror
* 定义报错函数 
* 定义的另一个函数, 如果该函数执行出错, 则执行报错函数

<br />

# 九. 高级 JavaScript 实例
### (1) 检测浏览器及版本
> `parseFloat()` 函数可解析一个字符串，并返回一个浮点数。
```html
<html>
<body>
<script type="text/javascript">
var browser=navigator.appName
var b_version=navigator.appVersion
var version=parseFloat(b_version)
document.write("浏览器名称："+ browser)
document.write("<br />")
document.write("浏览器版本："+ version)
</script>
</body>
</html>
```
返回: 
```
浏览器名称：Netscape
浏览器版本：5
```

### (2) 检测浏览器的更多信息
> 看看就行了, 了解一下
```html
document.write("<p>浏览器：")
document.write(navigator.appName + "</p>")

document.write("<p>浏览器版本：")
document.write(navigator.appVersion + "</p>")

document.write("<p>代码：")
document.write(navigator.appCodeName + "</p>")

document.write("<p>平台：")
document.write(navigator.platform + "</p>")

document.write("<p>Cookies 启用：")
document.write(navigator.cookieEnabled + "</p>")

document.write("<p>浏览器的用户代理报头：")
document.write(navigator.userAgent + "</p>")
```

### (3) 检测浏览器的全部信息
> emmm. 和上面大体是一样的, 需要用的时候自行百度


### (4) 根据浏览器类型提醒用户
```js
function detectBrowser()
{
var browser=navigator.appName
var b_version=navigator.appVersion
var version=parseFloat(b_version)
if ((browser=="Netscape"||browser=="Microsoft Internet Explorer") && (version>=4))
  {alert("您的浏览器够先进了！")}
else
  {alert("是时候升级您的浏览器了！")}
}
```

> 后面的高级实例不想看了, 感觉用不上.


> 看了一些项目的 JS 代码. 看起来好复杂啊.......
