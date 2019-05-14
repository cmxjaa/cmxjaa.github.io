---
layout: post
title: "HTML表单"
date: 2019-03-31
author: duckduckk
category: 2019-03
tags: web
finished: true
---


[参考w3school-HTML表单](http://www.w3school.com.cn/html/html_forms.asp)




# 一, HTML 表单
> 这一部分说的比较乱, 我随便写写


### (1) `<form>` 元素
HTML 表单用于收集用户输入。
`<form>` 元素定义 HTML 表单

### (2) `<input>` 元素
`<input>` 元素是最重要的表单元素。

本章中使用的类型:
* text	定义常规文本输入。
* radio	定义单选按钮输入（选择多个选择之一）
* submit	定义提交按钮（提交表单）

### (3) 文本输入
`<input type="text">` 定义用于文本输入的单行输入字段：
```html
<form>
 First name:<br>
<input type="text" name="firstname">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 
```

### (4) 单选按钮输入
`<input type="radio">` 定义单选按钮。

单选按钮允许用户在有限数量的选项中选择其中之一
```html
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form>
```

### (5) 提交按钮
`<input type="submit">` 定义用于向表单处理程序（form-handler）提交表单的按钮。

表单处理程序通常是包含用来处理输入数据的脚本的服务器页面。

表单处理程序在表单的 action 属性中指定：
```html
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 
```

### (6) Action 属性
* action 属性定义在提交表单时执行的动作。
* 向服务器提交表单的通常做法是使用提交按钮。
* 通常，表单会被提交到 web 服务器上的网页。
* 如果省略 action 属性，则 action 会被设置为当前页面

```html
<form action="action_page.php">
```

### (7) html
```html
<form action="action_page.php" method="GET">
```
或：
```html
<form action="action_page.php" method="POST">
```

### (8) GET和POST
GET(默认方法):

* 如果表单提交是被动的（比如搜索引擎查询），并且没有敏感信息。
* 表单数据在页面地址栏中是可见的：
* GET 最适合少量数据的提交。浏览器会设定容量限制。

POST: 
* 如果表单正在更新数据，或者包含敏感信息(例如密码)
* POST 的安全性更佳，因为在页面地址栏中被提交的数据是不可见的


### (9) Name 属性
如果要正确地被提交，每个输入字段必须设置一个 name 属性

### (10) `<fieldset>`
`<fieldset>` 元素组合表单中的相关数据
 
### (11) HTML Form 属性
HTML `<form>` 元素 

<br/>

# 二, HTML 表单元素

### (1) `<input>` 元素
* 最重要的表单元素是 `<input>` 元素。
* `<input>` 元素根据不同的 type 属性，可以变化为多种形态。

### (2) `<select>` 元素
`<select>` 元素定义下拉列表


### 另: `<option>` 元素
`<option>` 元素定义待选择的选项。

列表通常会把首个选项显示为被选选项。

可以通过添加 selected 属性来定义预定义选项

### (3) `<textarea>` 元素
`<textarea>` 元素定义多行输入字段(文本域)

### (4) `<button>` 元素
`<button>` 元素定义可点击的按钮：


```html
<button type="button" onclick="alert('Hello World!')">Click Me!</button>
```

### (5) HTML5 表单元素
HTML5 增加了如下表单元素：
* `<datalist>`
* `<keygen>`
* `<output>`

### (6) HTML5 `<datalist>` 元素
* `<datalist>` 元素为 `<input>` 元素规定预定义选项列表。
* 用户会在他们输入数据时看到预定义选项的下拉列表。
* `<input>` 元素的 list 属性必须引用 `<datalist>` 元素的 id 属性


<br/>

# 三, HTML 输入类型

描述 `<input>` 元素的输入类型

### (1) 输入类型：text
`<input type="text">` 定义供文本输入的单行输入字段

### (2) 输入类：password
`<input type="password">` 定义密码字段

密码字段中的字符被掩码(显示为星号或圆点)

### (3) 输入类型：submit
`<input type="submit">` 定义提交表单数据至表单处理程序的按钮。

表单处理程序(form-handler) 通常是包含处理输入数据的脚本的服务器页面。

在表单的 action 属性中规定表单处理程序 (form-handler), 如：

```html
<form action="action_page.php">
```

### (4) Input Type: radio
`<input type="radio">` 定义单选按钮

### (5) Input Type: checkbox
`<input type="checkbox">` 定义复选框。

复选框允许用户在有限数量的选项中选择零个或多个选项。

### (6) Input Type: button
`<input type="button>` 定义按钮。

<br/>

### 以下为HTML5 新增的输入类型

<br/>

### (7) 输入类型：number
`<input type="number">` 用于应该包含数字值的输入字段。

并能够对数字做出限制。

### (8) 输入限制

相关的输入限制有很多, 自行百度.

### (9) 输入类型：date
`<input type="date">` 用于应该包含日期的输入字段。

也可以向输入添加限制

### (10) 输入类型：color
`<input type="color">` 用于应该包含颜色的输入字段。

### (11) 输入类型：range
`<input type="range">` 用于应该包含一定范围内的值的输入字段。

根据浏览器支持，输入字段能够显示为滑块控件。

### (12) 输入类型：month
`<input type="month">` 允许用户选择 月份 和 年份.

### (13) 输入类型：week
`<input type="week">` 允许用户选择周和年。

### (14) 输入类型：time
`<input type="time">` 允许用户选择时间 (无时区)

### (15) 输入类型：datetime
`<input type="datetime">` 允许用户选择日期和时间(有时区)。
> 我试着输入了一下, 返回错误..emmm

### (16) 输入类型：datetime-local
`<input type="datetime-local">` 允许用户选择日期和时间(无时区)。

### (17) 输入类型：email
`<input type="email">` 用于应该包含电子邮件地址的输入字段。

根据浏览器支持，能够在被提交时自动对电子邮件地址进行**验证**

### (18) 输入类型：search
`<input type="search">` 用于搜索字段 (搜索字段的表现类似常规文本字段)

### (19) 输入类型：tel
`<input type="tel">` 用于应该包含电话号码的输入字段。

目前只有 Safari 8 支持 tel 类型。(注: 2019-03-31时我所看到文档是这样现实的)

### (20) 输入类型：url
`<input type="url">` 用于应该包含 URL 地址的输入字段。

根据浏览器支持，在提交时能够自动验证 url 字段。

<br/>

# 四, HTML 输入属性

### (1) value 属性
value 属性规定输入字段的初始值

### (2) readonly 属性
readonly 属性规定输入字段为只读 (不能修改)

### (3) disabled 属性
* disabled 属性规定输入字段是禁用的。
* 被禁用的元素是不可用和不可点击的。
* 被禁用的元素不会被提交。

### (4) size 属性
size 属性规定输入字段的尺寸 (以字符计)

### (5) maxlength 属性
maxlength 属性规定输入字段允许的最大长度

> size属性规定的时输入框的尺寸, 而maxlength规定的是输入字段的最大长度.

<br/>

### 以下为 HTML5 新增的输入属性
<br/>

### (6) autocomplete 属性
autocomplete 属性规定表单或输入字段是否应该自动完成。

当自动完成开启，浏览器会基于用户之前的输入值自动填写值。

可以把表单的 autocomplete 设置为 on，同时把特定的输入字段设置为 off，反之亦然。

### (7) novalidate 属性
novalidate 属性属于 `<form>` 属性。

如果设置，则 novalidate 规定在提交表单时不对表单数据进行验证。

### (8) autofocus 属性
autofocus 属性是布尔属性。

如果设置，则规定当页面加载时 `<input>` 元素应该自动获得焦点。

使 "First name" 输入字段在页面加载时自动获得焦点：
```html
First name:<input type="text" name="fname" autofocus>
```

### (9) form 属性
form 属性规定 `<input>` 元素所属的一个或多个表单

### (10) formaction 属性
formaction 属性规定当提交表单时处理该输入控件的文件的 URL。



### (11) formenctype 属性
formenctype 属性规定当把表单数据（form-data）提交至服务器时如何对其进行编码（仅针对 method="post" 的表单）。


### (12) formmethod 属性
formmethod 属性定义用以向 action URL 发送表单数据（form-data）的 HTTP 方法("get" or "post")

### (13) formnovalidate 属性
novalidate 属性是布尔属性。

如果设置，则规定在提交表单时不对 `<input>` 元素进行验证。

### (14) formtarget 属性
formtarget 属性规定的名称或关键词指示提交表单后在何处显示接收到的响应。

提交到新窗口:
```html
formtarget="_blank" 
```

### (15) height 和 width 属性
height 和 width 属性规定 `<input>` 元素的高度和宽度。

height 和 width 属性仅用于 `<input type="image">`

如果浏览器不清楚图像尺寸，则页面会在图像加载时闪烁。所以需要始终规定图像的尺寸。

### (16) list 属性
list 属性引用的 `<datalist>` 元素中包含了 `<input>` 元素的预定义选项。

### (17) min 和 max 属性
min 和 max 属性规定 `<input>` 元素的最小值和最大值。

### (18) multiple 属性
multiple 属性是布尔属性。

如果设置，则规定允许用户在 `<input>` 元素中输入一个以上的值。

multiple 属性适用于以下输入类型：email 和 file。

> multiple 属性可以用来提交文件

### (19) pattern 属性
pattern 属性规定用于检查 `<input>` 元素值的正则表达式。

输入三个从A到z的字符:

```html
pattern="[A-z]{3}  
```

### (20)placeholder 属性
placeholder 属性规定用以描述输入字段预期值的提示（样本值或有关格式的简短描述）

在输入框中显示 输入的要求
```html
placeholder="Search W3School"
```

### (20) required 属性
如果设置，则规定在提交表单之前必须填写输入字段。

此栏必填:
```html
required="required"
```

### (21) tep 属性
step 属性规定 `<input>` 元素的合法数字间隔。

如果 step="3"，则合法数字应该是 -3、0、3、6、等等。

```html
step="3"
```
