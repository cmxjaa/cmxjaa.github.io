---
layout: post
title: "CSS-Studying"
date: 2019-04-02
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> CSS   en 尽快把前端的HMTL CSS JS都看一遍.

> 先学CSS, 再顺便看一下CSS3

> CSS一共看了大概一天的时间, 终于看完了. 大创答辩结束, 难得有时间来学习. 晚上回来CSS还剩一点, 索性一鼓作气, 熬夜看完. 凌晨1点了, 我该睡了....

[参考W3School](http://www.w3school.com.cn/css/index.asp)

[参考菜鸟教程](http://www.runoob.com/css/css-tutorial.html)

# 一. CSS 基础教程

### (1) CSS 简介
* CSS 指层叠样式表 (Cascading Style Sheets)
* 样式定义如何显示 HTML 元素
* 样式通常存储在样式表中



### (2) CSS 基础语法

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。

```html
h1 {color:red; font-size:14px;}
```
* "h1" 为选择器
* "color:red","font-size:14px"为声明
* "color","font-size" 为属性
* "red","14px"为值


### (3) CSS 高级语法

#### 1, 选择器的分组


#### 2, 继承及其问题
* 根据 CSS，子元素从父元素继承属性。
* 但是旧的浏览器可能会忽略继承, 可以对子元素重新重建一个规则(了解即可)

### (4) CSS 派生选择器
派生选择器示例: (使列表中的 strong 元素变为斜体字，而不是通常的粗体字)
```cs
li strong {
    font-style: italic;
    font-weight: normal;
  }
```

<br/>

### (5) CSS id 选择器

id 选择器以 "#" 来定义

### (6) CSS 类选择器

在 CSS 中，类选择器以一个点号显示：
```cs
.center {text-align: center}
```

*类名的第一个字符不能使用数字*

**用处:**
* 和 id 一样，class 也可被用作派生选择器
```cs
.fancy td {
	color: #f60;
	background: #666;
	}
```
* 元素也可以基于它们的类而被选择
```cs
td.fancy {
	color: #f60;
	background: #666;
	}
```


### (7) CSS 属性选择器

#### 1, 属性选择器
为带有 title 属性的所有元素设置样式：
```cs
[title]
{
color:red;
}
```
应用:
```cs
<h2 title="Hello world">Hello world</h2>
```

#### 2, 属性和值选择器
为 title="W3School" 的所有元素设置样式：
```cs
[title=W3School]
{
border:5px solid blue;
}
```
应用同理

#### 3, 属性和值选择器 - 多个值
为包含指定值的 title 属性的所有元素设置样式。适用于由空格分隔的属性值：
```cs
[title~=hello] { color:red; }
```
应用:
```cs
<h2 title="hello world">Hello world</h2>
<p title="student hello">Hello W3School students!</h1>
```
> 即 只要字符串中有 "hello" 这个单词的都可以应用

同理的还有lang属性:
```cs
[lang|=en] { color:red; }
```

#### 4, 设置表单的样式
定义:
```cs
input[type="text"]
{
  width:150px;
  ...
}

input[type="button"]
{
  width:120px;
  ...
}
```
应用:
```cs
<form name="input" action="" method="get">
<input type="text" name="Name" value="Bill" size="20">
<input type="button" value="Example Button">

</form>
```

### (8) CSS创建

当读到一个样式表时，浏览器会根据它来格式化 HTML 文档。插入样式表的方法有三种：
#### 1, 外部样式表
通过改变一个文件来改变整个站点的外观。每个页面使用 `<link>` 标签链接到样式表。`<link>` 标签在（文档的）头部
```cs
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

#### 2, 内部样式表
```cs
<head>
<style type="text/css">
  hr {color: sienna;}
  p {margin-left: 20px;}
  body {background-image: url("images/back40.gif");}
</style>
</head>
```

#### 3, 内联样式
使用样式（style）属性实现。在 Style 属性中可以包含任何 CSS 属性
```cs
<p style="color: sienna; margin-left: 20px">
This is a paragraph
</p>
```
> 个人理解:
* 外部样式表: 通过CSS文件改变整个HTML文档的格式
* 内部样式表: 通过`<style>`标签实现HTML文档部分区域格式化
* 内联样式: 通过`style`属性来实现部分HTML文档的格式化

另: 当外部样式表和内部样式表冲突时, 内部样式表优先显示


*** 



# 二. CSS 背景

### (1) 背景颜色
* 使用 background-color 属性为元素设置背景色
  
### (2) 背景图像
* background-image 属性描述了元素的背景图像 
* 如果需要设置一个背景图像，必须为这个属性设置一个 URL 值

### (3) 背景图像 - 水平或垂直平铺
默认情况下 background-image 属性会在页面的水平或者垂直方向平铺。

可以定义图像只在水平方向平铺 (repeat-x):
```cs
background-repeat:repeat-x;
```
### (4) 背景图像- 设置定位与不平铺
* background-repeat属性: 平铺与否
* background-position属性: 图像在背景中的位置
```cs
body
{
background-image:url('img_tree.png');
background-repeat:no-repeat;
background-position:right top;
}
```

### (5) 背景- 简写属性
页面的背景颜色通过很多的属性来控制。
可以将这些属性合并在同一个属性中.

背景颜色的简写属性为 "background":
```cs
body {background:#ffffff url('img_tree.png') no-repeat right top;}
```

<br/>

# 三. CSS Text(文本)

### (1) 文本颜色
颜色属性被用来设置文字的颜色


* 十六进制值
* 一个RGB值
* 颜色的名称


```cs
body {color:red;}
h1 {color:#00ff00;}
h2 {color:rgb(255,0,0);}
```

### (2) 文本的对齐方式
文本排列属性是用来设置文本的水平对齐方式。

`text-align:justify`可用于正文
```cs
h1 {text-align:center;}
p.date {text-align:right;}
p.main {text-align:justify;}
```

### (3) 文本修饰
* 无修饰
* 上划线 (我自己是这样叫的...)
* 中划线
* 下划线

```cs
a {text-decoration:none;}
h1 {text-decoration:overline;}
h2 {text-decoration:line-through;}
h3 {text-decoration:underline;}
```

### (4) 文本转换
* 全都转换成大写
* 全都转换成小写
* 每个单词的首字母大写


```cs
p.uppercase {text-transform:uppercase;}
p.lowercase {text-transform:lowercase;}
p.capitalize {text-transform:capitalize;}
```

### (5) 文本缩进
文本缩进属性是用来指定文本的第一行的缩进。
```cs
p {text-indent:50px;}
```

<br/>

# 四, CSS Fonts(字体)

### (1) CSS字型
在CSS中，有两种类型的字体系列名称：

* 通用字体系列 - 拥有相似外观的字体系统组合（如 "Serif" 或 "Monospace"）
* 特定字体系列 - 一个特定的字体系列（如 "Times" 或 "Courier"）

### (2) 字体系列
font-family 属性设置文本的字体系列

font-family 属性应该设置几个字体名称作为一种"后备"机制，如果浏览器不支持第一种字体，他将尝试下一种字体。

> 如果字体名字为一个单词, 则不用引号; 如果为多个单词, 则需要用引号括起来.

```cs
p{font-family:"Times New Roman", Times, serif;}
```
### (3) 字体样式


* 正常 - 正常显示文本
* 斜体 - 以斜体字显示的文字
* 倾斜的文字 - 文字向一边倾斜（和斜体类似，但不太支持）
```cs
p.normal {font-style:normal;}
p.italic {font-style:italic;}
p.oblique {font-style:oblique;}
```

### (4) 设置字体大小像素
字体默认大小是16像素(16px=1em)
```cs
h1 {font-size:40px;}
h2 {font-size:30px;}
p {font-size:14px;}
```

### (5) 用em来设置字体大小
为了避免Internet Explorer 中无法调整文本的问题，许多开发者使用 em 单位代替像素.

字体默认大小为1em, 即16px.

转换公式: `px/16=em`
```cs
h1 {font-size:2.5em;} /* 40px/16=2.5em */
```

### (6) 使用百分比和EM组合
在所有浏览器的解决方案中，设置 `<body>`元素的默认字体大小的是百分比

```cs
body {font-size:100%;}
```

<br/>

# 五. CSS 链接 (link)

### (1) 链接样式
四种链接状态: 
* a:link - 正常，未访问过的链接
* a:visited - 用户已访问过的链接
* a:hover - 当用户鼠标放在链接上时
* a:active - 链接被点击的那一刻

```cs
a:link {color:#000000;}      /* 未访问链接*/
a:visited {color:#00FF00;}  /* 已访问链接 */
a:hover {color:#FF00FF;}  /* 鼠标移动到链接上 */
a:active {color:#0000FF;}  /* 鼠标点击时 */
```

顺序规则：

* a:hover 必须跟在 a:link 和 a:visited后面
* a:active 必须跟在 a:hover后面

### (2) 文本修饰
text-decoration 属性主要用于删除链接中的下划线：
> 上面这句话表达的意思不是很清楚, 但是具体意思看代码就会懂

```cs
a:link {text-decoration:none;}
a:visited {text-decoration:none;}
a:hover {text-decoration:underline;}
a:active {text-decoration:underline;}
```

### (3) 背景颜色
背景颜色属性指定链接背景色：
```cs
a:link {background-color:#B2FF99;}
a:visited {background-color:#FFFF85;}
a:hover {background-color:#FF704D;}
a:active {background-color:#FF704D;}
```

<br/>

# 六. CSS 列表样式(ul)
### (1) 列表
在HTML中，有两种类型的列表：
* 无序列表 - 列表项标记用特殊图形（如小黑点、小方框等）
* 有序列表 - 列表项的标记有数字或字母

### (2) 不同的列表项标记
list-style-type属性指定列表项标记的类型

以下代码中的`列表中的标记项`分别为:
* 圆圈 
* 方块
* 大写的罗马数字
* 小写的阿拉伯数字

```cs
ul.a {list-style-type: circle;}
ul.b {list-style-type: square;}
 
ol.c {list-style-type: upper-roman;}
ol.d {list-style-type: lower-alpha;}
```

### (3) 作为列表项标记的图像
```cs
ul
{
    list-style-image: url('sqpurple.gif');
}
```

> 有序列表<`ol>`和无序列表`<ul>`中使用`<li>`标签定义列表项目

### (4) 浏览器兼容性解决方案
> 上面的例子在所有浏览器中显示并不相同, 所以需要考虑浏览器兼容问题


代码解释:
ul:
* 设置列表样式类型为没有删除列表项标记
* 设置填充和边距0px（浏览器兼容性）

ul中所有li:
* 设置图像的URL，并设置它只显示一次（无重复）
* 需要的定位图像位置（左0px和上下5px）
* 用padding-left属性把文本置于列表中

```cs
ul
{
    list-style-type: none;
    padding: 0px;
    margin: 0px;
}
ul li
{
    background-image: url(sqpurple.gif);
    background-repeat: no-repeat;
    background-position: 0px 5px; 
    padding-left: 14px; 
}
```

### (5) 列表 -简写属性
```cs
ul
{
    list-style: square url("sqpurple.gif");
}
```

顺序:
* list-style-type
* list-style-position (有关说明，请参见下面的CSS属性表)
* list-style-image


<br/>

# 七, CSS Table(表格)

### (1) 表格边框
代码解释:
* 指定CSS表格边框，使用border属性。
* 指定了一个表格的Th和TD元素的黑色边框
* 该表格有双边框。这是因为表和th/ td元素有独立的边界

```cs
table, th, td
{
    border: 1px solid black;
}
```

### (2) 折叠边框
* border-collapse属性可设置表格边框是否折叠成一个单一的边框或隔开
* 该段代码可去掉双边框, 展现出单边框.
```cs
table
{
    border-collapse:collapse;
}
```

### (3) 表格宽度和高度
Width和height属性定义表格的宽度和高度。

```cs
table 
{
    width:100%;
}
th
{
    height:50px;
}
```

### (4) 表格文字对齐
text-align属性设置水平对齐方式，向左，右，或中心：
```cs
td
{
    text-align:right;
}
```

vertical-align属性设置垂直对齐，比如顶部，底部或中间：
```cs
td
{
    height:50px;
    vertical-align:bottom;
}
```

### (5) 表格填充
> 个人理解: 所谓表格填充, 就是通过填充 控制表格里面每个小框框的大小

```cs
td
{
    padding:15px;
}
```

### (6) 表格颜色
* 指定边框的颜色，
* 指定th元素的文本和背景颜色

```cs
table, td, th
{
    border:1px solid green;
}
th
{
    background-color:green;
    color:white;
}
```

<br/>

# 八. CSS 盒子模型

### (1) CSS 盒子模型 (Box Model)

CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。
* Margin(外边距) - 清除边框外的区域，外边距是透明的。
* Border(边框) - 围绕在内边距和内容外的边框。
* Padding(内边距) - 清除内容周围的区域，内边距是透明的。
* Content(内容) - 盒子的内容，显示文本和图像。

菜鸟教程的图:

![img](http://www.runoob.com/images/box-model.gif)

### (2) 元素的宽度和高度
> 重要: 当指定一个CSS元素的宽度和高度属性时，只是设置内容区域的宽度和高度。对于完全大小的元素，还必须添加填充，边框和边距。

下面的例子中的元素的总宽度为300px：
而完全大小的元素为450px:
300px (宽)
+50px (左 + 右填充)
+50px (左 + 右边框)
+50px (左 + 右边距)
=450px
```cs
div {
    width: 300px;
    border: 25px solid green;
    padding: 25px;
    margin: 25px;
}
```

* 最终元素的总宽度计算公式是这样的：
总元素的宽度=宽度+左填充+右填充+左边框+右边框+左边距+右边距
* 元素的总高度最终计算公式是这样的：
总元素的高度=高度+顶部填充+底部填充+上边框+下边框+上边距+下边距

<br/>

# 九. CSS Border (边框)

### (1) 边框样式
border-style属性用来定义边框的样式

根据border-style值的不同定义不同的边框属性, 该属性的值太多, 需要用的时候可以查资料.


### (2) 边框宽度
可以通过 border-width 属性为边框指定宽度。

为边框指定宽度有两种方法：
* 指定长度值，比如 2px 或 0.1em等
* 或者使用 3 个关键字:thick,medium（默认值） ,thin.
* 三个关键字的大小根据用户设置的不同, 大小可能不定.
```cs
 border-width:5px;
 ```

### (3) 边框颜色
border-color属性用于设置边框的颜色。可以设置的颜色：
* name - 指定颜色的名称，如 "red"
* RGB - 指定 RGB 值, 如 "rgb(255,0,0)"
* Hex - 指定16进制值, 如 "#ff0000"

border-color单独使用是不起作用的，必须得先使用border-style来设置边框样式。

```cs
p.one
{
    border-style:solid;
    border-color:red;
}
```

### (4) 边框-单独设置各边
在CSS中，可以指定不同的侧面不同的边框：
```cs
p
{
    border-top-style:dotted;
    border-right-style:solid;
    border-bottom-style:dotted;
    border-left-style:solid;
}
```

### (5) 边框-简写属性
* 边框宽度为5像素
* 边框样式为solid
* 边框颜色为red
  

```cs
border:5px solid red;
```

<br/>

# 十. CSS轮廓 (outline) 属性

轮廓（outline）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

> 个人理解: 轮廓不在四大件里面(内容,内边距,边框,外边距)
> 个人理解: 内容与内边距之间的即使 填充

### (1) 所有CSS 轮廓（outline）属性
* outline 在一个声明中设置所有的轮廓属性
* outline-color 设置轮廓的颜色
* outline-style 设置轮廓的样式
* outline-width 设置轮廓的宽度

<br/>

# 十一. CSS margin (外边距)

margin 清除周围的（外边框）元素区域。margin 没有背景颜色，是完全透明的。

菜鸟教程图:

![img](http://www.runoob.com/wp-content/uploads/2013/08/VlwVi.png)

### (1) Margin - 单边外边距属性
在CSS中，它可以指定不同的侧面不同的边距：
```cs
margin-top:100px;
margin-bottom:100px;
margin-right:50px;
margin-left:50px;
```

### (2) Margin - 简写属性
所有边距属性的简写属性是 margin :
* 上下边距为100px
* 左右边距为50px
```cs
margin:100px 50px;
```

<br/>

# 十二. CSS padding (填充)
> **填充即内边距**

### (1) 填充- 单边内边距属性
在CSS中，它可以指定不同的侧面不同的填充：
```cs
padding-top:25px;
padding-bottom:25px;
padding-right:50px;
padding-left:50px;
```

### (2) 填充 - 简写属性
简写属性是 padding :
* 上下填充为25px
* 左右填充为50px


```cs
padding:25px 50px;
```

<br/>

# 十三. CSS 分组和嵌套
### (1) 分组选择器

在样式表中有很多具有相同样式的元素。
```cs
h1
{
    color:green;
}
h2
{
    color:green;
}
p
{
    color:green;
}
```
为减少代码, 可以使用分组选择器, 变成如下模样:
```cs
h1,h2,p
{
    color:green;
}
```
### (2) 嵌套选择器
> 看CSS基础教程的时候, 就不知道这三个有什么区别. 现在懂了.

* `p{ }`: 为所有 p 元素指定一个样式。
* `.marked{ }`: 为所有 class="marked" 的元素指定一个样式。
* `.marked p{ }`: 为所有 class="marked" 元素内的 p 元素指定一个样式。
* `p.marked{ }`: 为所有 class="marked" 的 p 元素指定一个样式。

```cs
p
{
    color:blue;
    text-align:center;
}
.marked
{
    background-color:red;
}
.marked p
{
    color:white;
}
p.marked{
    text-decoration:underline;
}
```

<br/>

# 十四. CSS 尺寸
CSS 尺寸 (Dimension) 属性可以控制元素的高度和宽度. 同时也可以增加行间距.

所有CSS 尺寸 (Dimension)属性: 
* height	设置元素的高度。
* line-height	设置行高。
* max-height	设置元素的最大高度。
* max-width	设置元素的最大宽度。
* min-height	设置元素的最小高度。
* min-width	设置元素的最小宽度。
* width	设置元素的宽度。


<br/>

# 十五. CSS Display(显示) 与 Visibility（可见性）
display属性设置一个元素应如何显示，visibility属性指定一个元素应可见还是隐藏

### (1) 隐藏元素
实现方法:
* display:none
* visibility:hidden

visibility:hidden可以隐藏某个元素，但该元素仍占用一定的控制, 影响布局。
display:none可以隐藏某个元素，且隐藏的元素不会占用任何空间.

> 个人理解: visibility:hidden 展现了该元素, 只是没有让你看见, 所以会影响布局.
> display:none 压根就没有展现该元素, 所以不会影响布局.


### (2) CSS Display - 块和内联元素
块元素是一个元素，占用了全部宽度，在前后都是换行符。
块元素的例子：
```cs
<h1>
<p>
<div>
```

内联元素只需要必要的宽度，不强制换行。
内联元素的例子：
```cs
<span>
<a>
```

### (3) 改变一个元素显示

把列表项显示为内联元素：
```cs
li {display:inline;}
```

把span元素作为块元素：
```cs
span {display:block;}
```

<br/>

# 十六. CSS Position (定位)
position 属性指定了元素的定位类型。

position 属性的五个值：
* static
* relative
* fixed
* absolute
* sticky


### (1) static 定位
HTML 元素的默认值，即没有定位，遵循正常的文档流对象。

静态定位的元素不会受到 top, bottom, left, right影响。
```cs
div.static {
    position: static;
    border: 3px solid #73AD21;
}
```

### (2) fixed 定位
元素的位置相对于浏览器窗口是固定位置。

即使窗口是滚动的它也不会移动：
```cs
p.pos_fixed
{
    position:fixed;
    top:30px;
    right:5px;
}
```

### (3) relative 定位
**相对定位元素**的定位是相对其正常位置。
```cs
h2.pos_left
{
    position:relative;
    left:-20px;
}
h2.pos_right
{
    position:relative;
    left:20px;
}
```

### (4) absolute 定位
绝对定位
> 个人理解: absolute 定位定位于页面, fixed定位定位于屏幕


```cs
h2
{
    position:absolute;
    left:100px;
    top:150px;
}
```

### (5) sticky 定位
position: sticky; 基于用户的滚动位置来定位

```cs
div.sticky {
    position: -webkit-sticky; /* Safari */
    position: sticky;
    top: 0;
    background-color: green;
    border: 2px solid #4CAF50;
}
```


### (6) 重叠的元素
当`z-index:-1;`时, 该元素的显示放在后面. 当为其他值时, 该元素的显示放在前面

```cs
z-index:-1;
```

### (7) 其他
不属于本次学习的内容, 但是觉得挺好玩的.

[改变光标](http://www.runoob.com/try/try.php?filename=trycss_cursor)


<br/>

# 十七. CSS Overflow
CSS overflow 属性用于控制内容溢出元素框时显示的方式。

### (1) CSS Overflow
overflow有以下值:
* visible	默认值。内容不会被修剪，会呈现在元素框之外。
* hidden	内容会被修剪，并且其余内容是不可见的。
* scroll	内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容。
* auto	如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。
* inherit	规定应该从父元素继承 overflow 属性的值。


### (2) overflow: visible
默认情况下，overflow 的值为 visible， 意思是内容溢出元素框

<br/>

# 十八. CSS Float (浮动)

* CSS 的 Float（浮动），会使元素向左或向右移动，其周围的元素也会重新排列。
* Float（浮动），往往是用于图像，但它在布局时一样非常有用。
* 元素只能左右移动而不能上下移动。
* 浮动元素之后的元素将围绕它。
### (1) 元素怎么浮动

下面的代码中, 图像是右浮动，文本流将环绕在它左边：
```cs
img
{
    float:right;
}
```

### (2) 彼此相邻的浮动元素

把几个浮动的元素放到一起，如果有空间的话，它们将彼此相邻。

### (3) 清除浮动 - 使用 clear
元素浮动之后，周围的元素会重新排列，为了避免这种情况，使用 clear 属性。

clear 属性指定元素两侧不能出现浮动元素。
```cs
.text_line
{
    clear:both;
}
```

<br/>

# 十九. CSS 对齐

### (1) 元素居中对齐
* 要水平居中对齐一个元素, 可以使用 `margin: auto;`
* 如果没有设置 width 属性(或者设置 100%)，居中对齐将不起作用。

### (2) 文本居中对齐
使文本在元素内居中对齐, 可以使用`text-align:center;`

### (3) 图片居中对齐
要让图片居中对齐, 可以使用 margin: auto; 并将它放到 块 元素中:
```cs
img {
    display: block;
    margin: auto;
    width: 40%;
}
```

### (4) 左右对齐 - 使用定位方式
使用 position: absolute; 属性来对齐元素:

右对齐:
```cs
.right {
    position: absolute;
    right: 0px;
    width: 300px;
    border: 3px solid #73AD21;
    padding: 10px;
}
```

当使用 position 来对齐元素时, 通常 `<body>` 元素会设置 margin 和 padding 
```cs
body {
    margin: 0;
    padding: 0;
}
```

### (5) 左右对齐 - 使用 float 方式
也可以使用 float 属性来对齐元素:
```cs
.right {
    float: right;
    width: 300px;
    border: 3px solid #73AD21;
    padding: 10px;
}
```
另外: 如果子元素的高度大于父元素，且子元素设置了浮动，那么子元素将溢出，可以使用 "clearfix(清除浮动)" 来解决该问题。

可以在父元素上添加 overflow: auto; 来解决子元素溢出的问题:
```cs
.clearfix {
    overflow: auto;
}
```

### (6) 垂直居中对齐 - 使用 padding
头部顶部使用 padding实现垂直居中对齐

注意padding值里面的0, 正是这个0实现了垂直居中对齐
```cs
.center {
    padding: 70px 0;
    border: 3px solid green;
}
```

如果要水平和垂直都居中，可以使用 padding 和 text-align: center: 
```cs
.center {
    padding: 70px 0;
    border: 3px solid green;
    text-align: center;
}
```

### (7) 垂直居中 - 使用 line-height
> 没太看懂

```cs
.center {
    line-height: 200px;
    height: 200px;
    border: 3px solid green;
    text-align: center;
}
 
/* 如果文本有多行，添加以下代码: */
.center p {
    line-height: 1.5;
    display: inline-block;
    vertical-align: middle;
}
```

### (8) 垂直居中 - 使用 position 和 transform
```cs
.center p {
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

<br/>

# 二十. CSS组合选择符
组合选择符说明了两个选择器直接的关系。

在 CSS3 中包含了四种组合方式:

* 后代选择器(以空格分隔)
* 子元素选择器(以大于号分隔）
* 相邻兄弟选择器（以加号分隔）
* 普通兄弟选择器（以破折号分隔）

### (1) 后代选择器
后代选择器用于选取某元素的后代元素。

以下实例选取所有 `<p>` 元素插入到 `<div>` 元素中: 
```cs
div p
{
  background-color:yellow;
}
```

### (2) 子元素选择器
与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素

以下实例选择了`<div>`元素中所有直接子元素 `<p>` ：
```cs
div>p
{
  background-color:yellow;
}
```

> 个人理解: 后代选择器只要插入在里面就行了, 而子元素选择器则是 直接子元素才行(只能直接插入, 不能间接插入)

### (3) 相邻兄弟选择器

如果需要选择紧接在另一个元素后的元素，而且二者有相同的父元素，则可以使用相邻兄弟选择器

以下实例选取了所有位于 `<div>` 元素后的第一个 `<p>` 元素:
```cs
div+p
{
  background-color:yellow;
}
```

### (4) 后续兄弟选择器
后续兄弟选择器选取所有指定元素之后的相邻兄弟元素。

以下实例选取了所有 `<div>` 元素之后的所有相邻兄弟元素 `<p>` : 
```cs
div~p
{
  background-color:yellow;
}
```

<br/>

# 二十一. CSS 伪类
CSS伪类是用来添加一些选择器的特殊效果

### (1) 语法
伪类的语法：
```cs
selector:pseudo-class {property:value;}
```
CSS类也可以使用伪类：
```cs
selector.class:pseudo-class {property:value;}
```

### (2) anchor伪类
```cs
a:link {color:#FF0000;} /* 未访问的链接 */
a:visited {color:#00FF00;} /* 已访问的链接 */
a:hover {color:#FF00FF;} /* 鼠标划过链接 */
a:active {color:#0000FF;} /* 已选中的链接 */
```

顺序:
在CSS定义中，a:hover 必须被置于 a:link 和 a:visited 之后，才是有效的。
在CSS定义中，a:active 必须被置于 a:hover 之后，才是有效的。

### (3) 伪类和CSS类
> 没太看懂


伪类可以与 CSS 类配合使用：
```cs
a.red:visited {color:#FF0000;}
 
<a class="red" href="css-syntax.html">CSS 语法</a>
```
如果在上面的例子的链接已被访问，它会显示为红色。

### (4) CSS :first-child 伪类
可以使用 :first-child 伪类来选择父元素的第一个子元素

### (5) 匹配第一个 `<p>` 元素
在下面的例子中，选择器匹配作为任何元素的第一个子元素的 `<p>` 元素：
```cs
p:first-child
{
    color:blue;
}
```

### (6) 匹配所有`<p>` 元素中的第一个 `<i>` 元素
在下面的例子中，选择相匹配的所有`<p>`元素的第一个 `<i>` 元素：
```cs
p > i:first-child
{
    color:blue;
}
```

### (7) 匹配所有作为第一个子元素的 `<p>` 元素中的所有 `<i>` 元素
在下面的例子中，选择器匹配所有作为元素的第一个子元素的 `<p>` 元素中的所有 `<i>` 元素：
```cs
p:first-child i
{
    color:blue;
}
```

> (6)和(7)的区别: (6)是p中的 i 的第一个子元素颜色为蓝, (7)是p的第一个子元素的 i 颜色为蓝

### (8) CSS - :lang 伪类
lang 类为属性值为 no 的q元素定义引号的类型：
```cs
q:lang(no) {quotes: "~" "~";}
```

<br/>

# 二十二. CSS 伪元素
CSS伪元素是用来添加一些选择器的特殊效果。

### (1) 语法
伪元素的语法：
```cs
selector:pseudo-element {property:value;}
```
CSS类也可以使用伪元素：
```cs
selector.class:pseudo-element {property:value;}
```

### (2) :first-line 伪元素
"first-line" 伪元素用于向文本的首行设置特殊样式。

在下面的例子中，浏览器会根据 "first-line" 伪元素中的样式对 p 元素的第一行文本进行格式化：
```cs
p:first-line 
{
    color:#ff0000;
    font-variant:small-caps;
}
```
### (3) :first-letter 伪元素
"first-letter" 伪元素用于向文本的首字母设置特殊样式：
```cs
p:first-letter 
{
    color:#ff0000;
    font-size:xx-large;
}
```

### (4) 伪元素和CSS类
伪元素可以结合CSS类 

在下面的例子中,会使所有 class 为 article 的段落的首字母变为红色:
```cs
p.article:first-letter {color:#ff0000;}

<p class="article">文章段落</p>
```

### (5) 多个伪元素
可以结合多个伪元素来使用

在下面的例子中:
* 段落的第一个字母将显示为红色，其字体大小为 xx-large
* 第一行中的其余文本将为蓝色，并以小型大写字母显示
* 段落中的其余文本将以默认字体大小和颜色来显示

```cs
p:first-letter
{
    color:#ff0000;
    font-size:xx-large;
}
p:first-line 
{
    color:#0000ff;
    font-variant:small-caps;
}
```

### (6) CSS - :before 伪元素
":before" 伪元素可以在元素的内容前面插入新内容。

在每个 `<h1>`元素前面插入一幅图片：
```cs
h1:before 
{
    content:url(smiley.gif);
}
```

### (7) CSS - :after 伪元素
":after" 伪元素可以在元素的内容之后插入新内容。

在每个 `<h1>` 元素后面插入一幅图片：
```cs
h1:after
{
    content:url(smiley.gif);
}
```

<br/>

# 二十三. CSS 导航栏

### (1) 导航栏=链接列表
导航条基本上是一个链接列表，所以使用 `<ul>` 和 `<li>`元素非常有意义：

真实部署时, "#home"应该为真实的 url
```cs
<ul>
  <li><a href="#home">主页</a></li>
  <li><a href="#news">新闻</a></li>
  <li><a href="#contact">联系</a></li>
  <li><a href="#about">关于</a></li>
</ul>
```

删除列表标记,删除边距和填充:
```cs
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}
```
### (2) 垂直导航条实例
```cs
/* 确定整个无序列表的样式*/
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    width: 200px;
    background-color: #f1f1f1;
}

/* 确定链接的样式*/ 
li a {
    display: block;
    color: #000;
    padding: 8px 16px;
    text-decoration: none;
}
 
/* 鼠标移动到选项上修改背景颜色 */
li a:hover {
    background-color: #555;
    color: white;
}
```

### (3) 激活/当前导航条实例
添加 "active" 类来标准哪个选项被选中：

> 默认某一条是被选中的, 添加一个类来确定其样式

```cs
.active {
    background-color: #4CAF50;
    color: white;
}
```

### (4) 创建链接并添加边框
```cs
/*为每个边框添加边框*/
ul {
    border: 1px solid #555;
}
/* 让链接居中*/ 
li {
    text-align: center;
    border-bottom: 1px solid #555;
}
/* 取消最后一个子元素的下边框,因为前面已经添加了边框, 会重复叠加, 阴影加深*/ 
li:last-child {
    border-bottom: none;
}
```

###  (5) 全屏高度的固定导航条
创建一个左边是全屏高度的固定导航条，右边是可滚动的内容:
```cs
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    width: 25%;
    background-color: #f1f1f1;
    height: 100%; /* 全屏高度 */
    position: fixed; 
    overflow: auto; /* 如果导航栏选项多，允许滚动 */
}
```

该实例可以在移动设备上使用

> 以上为垂直导航栏, 以下为水平导航栏. 

### (6 ) 水平导航栏

有两种方法创建横向导航栏。使用内联(inline)或浮动(float)的列表项。

> 段落元素(自动转行)与内联元素(不自动转行)之间可以相互转化

### (7) 内联列表项
```cs
li
{
    display:inline;
}
```

### (8) 浮动列表项
* 浮动 `<li>`元素
* 指定为 `<a>`元素的宽度
<br/>
* float:left - 使用浮动块元素的幻灯片彼此相邻
* display:block - 显示块元素的链接，让整体变为可点击链接区域（不只是文本），它允许我们指定宽度
* width:60px - 块元素默认情况下是最大宽度。我们要指定一个60像素的宽度

```cs
li
{
    float:left;
}
a
{
    display:block;
    width:60px;
}
```

### (9) 链接右对齐
将导航条最右边的选项设置右对齐 (float:right;)
```cs
<ul>
...
  <li style="float:right"><a class="active" href="#about">关于</a></li>
</ul>
```

### (10) 添加分割线
`<li>` 通过 border-right 样式来添加分割线:
```cs
/* 除了最后一个选项(last-child) 其他的都添加分割线 */
li {
    border-right: 1px solid #bbb;
}
 
li:last-child {
    border-right: none;
}
```

### (11) 固定导航条
可以设置页面的导航条固定在头部或者底部

固定在头部:
```cs
ul {
    position: fixed;
    top: 0;
    width: 100%;
}
```

固定在底部:
```cs
ul {
    position: fixed;
    bottom: 0;
    width: 100%;
}
```

<br/>

# 二十四. CSS 下拉菜单

### (1) 基本下拉菜单
当鼠标移动到指定元素上时，会出现下拉菜单。

```cs
<style>
.dropdown {
    position: relative;
    display: inline-block;
}

.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    padding: 12px 16px;
    z-index: 1;
}

.dropdown:hover .dropdown-content {
    display: block;
}
</style>

<div class="dropdown">
  <span>Mouse over me</span>
  <div class="dropdown-content">
    <p>Hello World!</p>
  </div>
</div>
```

* .dropdown 类使用 position:relative, 这将设置下拉菜单的内容放置在下拉按钮 (使用 position:absolute) 的右下角位置。
* .dropdown-content 类中是实际的下拉菜单。默认是隐藏的，在鼠标移动到指定元素后会显示。
* 使用 box-shadow 属性让下拉菜单看起来像一个"卡片"。
* :hover 选择器用于在用户将鼠标移动到下拉按钮上时显示下拉菜单。

> 有两个`<div>`元素, 其中一个包含dropdown, 再在里面创建一个`<div>`元素, 包含dropdown-content.这样就把两者联系起来了.


### (2) 下拉内容对齐方式
* float:left;
* float:right;

<br/>

# 二十五. CSS 提示工具
提示工具在鼠标移动到指定元素后触发

基础提示框(Tooltip)
```html
<style>
/* Tooltip 容器 */
.tooltip {
    position: relative;
    display: inline-block;
    border-bottom: 1px dotted black; /* 悬停元素上显示点线 */
}
 
/* Tooltip 文本 */
.tooltip .tooltiptext {
    visibility: hidden;
    width: 120px;
    background-color: black;
    color: #fff;
    text-align: center;
    padding: 5px 0;
    border-radius: 6px;
 
    /* 定位 */
    position: absolute;
    z-index: 1;
}
 
/* 鼠标移动上去后显示提示框 */
.tooltip:hover .tooltiptext {
    visibility: visible;
}
</style>
 
<div class="tooltip">鼠标移动到这
  <span class="tooltiptext">提示文本</span>
</div>
```

* tooltip 类使用 position:relative, 提示文本需要设置定位值 position:absolute。
* tooltiptext的模式是隐藏的`visibility: hidden;`
* :hover 选择器用于在鼠标移动到到指定元素 `<div>` 上时显示的提示


### (2) 定位提示工具
显示在右侧：
```cs
.tooltip .tooltiptext {
    top: -5px;
    left: 105%; 
}
```


显示在左侧：
```cs
.tooltip .tooltiptext {
    top: -5px;
    right: 105%; 
}
```
显示在头部：
```cs
.tooltip .tooltiptext {
    width: 120px;
    bottom: 100%;
    left: 50%; 
    margin-left: -60px; /* 使用一半宽度 (120/2 = 60) 来水平居中提示工具 */
}
```

显示在底部：
```cs
.tooltip .tooltiptext {
    width: 120px;
    top: 100%;
    left: 50%; 
    margin-left: -60px; /* 使用一半宽度 (120/2 = 60) 来水平居中提示工具 */
}
```

### (3) 添加箭头
* 用CSS 伪元素`::after`及`content`属性为提示工具创建一个小箭头标志
* 箭头是由边框组成的，但组合起来后提示工具像个语音信息框
```cs
.tooltip .tooltiptext::after {
    content: " ";
    position: absolute;
    top: 100%; /* 提示工具底部 */
    left: 50%;
    margin-left: -5px;
    border-width: 5px;
    border-style: solid;
    border-color: black transparent transparent transparent;
}
```

border-color 用于将内容转换为箭头


提示工具头部,底部,左侧,右侧都可以显示箭头,具体看教程.

### (4) 淡入效果
使用 CSS3 transition 属性及 opacity 属性来实现提示工具的淡入效果:
```cs
.tooltip .tooltiptext {
    opacity: 0;
    transition: opacity 1s;
}
 
.tooltip:hover .tooltiptext {
    opacity: 1;
}
```

<br/>

# 二十六. CSS 图片廊
### (1) 图片廊
使用 CSS 创建图片廊：(将该段代码重复下去,就可以显示一排的图片)
```cs
<div class="responsive">
  <div class="img">
    <a target="_blank" href="http://static.runoob.com/images/demo/demo1.jpg">
      <img src="http://static.runoob.com/images/demo/demo1.jpg" alt="图片文本描述" width="300" height="200">
    </a>
    <div class="desc">这里添加图片文本描述</div>
  </div>
</div>
```
### (2) 响应式图片廊
> 我是没看出来有啥区别

<br/>

# 二十七. 图像透明/不透明

### (1) 创建一个透明图像
CSS3中属性的透明度是 `opacity`

Opacity属性值从0.0 - 1.0。值越小，使得元素更加透明
```cs
img
{
  opacity:0.4;
  filter:alpha(opacity=40); /* IE8 及其更早版本 */
}
```
### (2) 图像的透明度 - 悬停效果
```cs
img
{
  opacity:0.4;
  filter:alpha(opacity=40); /*  IE8 及其更早版本 */
}
img:hover
{
  opacity:1.0;
  filter:alpha(opacity=100); /* IE8 及其更早版本 */
}
```

### (3) 透明的盒子中的文字
> 代码是看懂了, 但是貌似没啥用

<br/>

# 二十八. CSS 图像拼合技术

### (1) 图像拼合 - 简单实例
与其使用三个独立的图像，不如我们使用这种单个图像("img_navsprites.gif"):

> 虽然知道代码是怎么回事, 但是没太看明白


```cs
img.home
{
width:46px;
height:44px;
background:url(img_navsprites.gif) 0 0;
}
```
```cs
<img class="home" src="/images/img_trans.gif"><br><br>
<img class="next" src="/images/img_trans.gif">
```

### (2) 图像拼合 - 创建一个导航列表
使用一个HTML列表，因为它可以链接，同时还支持背景图像：

```cs
#navlist{position:relative;}
#navlist li{margin:0;padding:0;list-style:none;position:absolute;top:0;}
#navlist li, #navlist a{height:44px;display:block;}

#home{left:0px;width:46px;}
#home{background:url('img_navsprites.gif') 0 0;}

#prev{left:63px;width:43px;}
#prev{background:url('img_navsprites.gif') -47px 0;}
```

```cs
<ul id="navlist">
  <li id="home"><a href="/"></a></li>
  <li id="prev"><a href="/css/"></a></li>
</ul>
```

### (3) 图像拼合s - 悬停效果
`:hover` 选择器用于鼠标悬停在元素上的显示的效果
对于上例, 我们添加悬停效果只添加两行代码：
```cs
#home a:hover{background: url('img_navsprites_hover.gif') 0 -45px;}
#prev a:hover{background: url('img_navsprites_hover.gif') -47px -45px;}
```

<br/>

# 二十九. CSS媒体类型

### (1) @media 规则
@media 规则允许在相同样式表为不同媒体设置不同的样式
```cs
@media screen
{
    p.test {font-family:verdana,sans-serif;font-size:14px;}
}
@media print
{
    p.test {font-family:times,serif;font-size:10px;}
}
@media screen,print
{
    p.test {font-weight:bold;}
}
```

### (2) 其他媒体类型
有很多, 自己看文档

<br/>

# 三十. CSS 属性选择器
### (1) 属性选择器
下面的例子是把包含标题(title)的所有元素变为蓝色：
```cs
[title]
{
    color:blue;
}
```

### (2) 属性和值选择器
下面的实例改变了标题title='runoob'元素的边框样式:
```cs
[title=runoob]
{
    border:5px solid green;
}
```

### (3) 属性和值的选择器 - 多值
下面是包含指定值的title属性的元素样式的例子，使用（~）分隔属性和值:

```cs
[title~=hello] { color:blue; }
```

下面是包含指定值的lang属性的元素样式的例子，使用（|）分隔属性和值:
```cs
[lang|=en] { color:blue; }
```

### (4) 表单样式
属性选择器样式无需使用class或id的形式:
```cs
input[type="text"]
{
    width:150px;
    display:block;
    margin-bottom:10px;
    background-color:yellow;
}
input[type="button"]
{
    width:120px;
    margin-left:35px;
    display:block;
}
```

> END

