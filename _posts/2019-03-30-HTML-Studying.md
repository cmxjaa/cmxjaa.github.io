---
layout: post
title: "HTML-Studying"
date: 2019-03-30
author: duckduckk
category: 2019-03
tags: web
finished: true
---

> HTML学习, 随便写写的目的在于提升当时看文档的效率,应该很快就可以看完.
> 愈发觉得博客写得太详细就会成为.....

[参考 W3school](http://www.w3school.com.cn/html/index.asp)

# 一, HTML 基础

### (1) HTML 标题
HTML 标题（Heading）是通过 `<h1> - <h6>` 等标签进行定义的

### (2) HTML 段落
HTML 段落是通过 `<p>` 标签进行定义的

### (3) HTML 链接
* HTML 链接是通过 `<a>` 标签进行定义的
* 注: 在 `href` 属性中指定链接的地址

### (4) HTML 图像
* HTML 图像是通过 `<img>` 标签进行定义的。
* 注: 图像的名称和尺寸是以属性的形式提供的

<br/>

# 二, HTML 元素

HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

例如,下面的`This is a paragraph`就是一个元素内容.
```html
<p>	This is a paragraph	</p>
```

### (1) `<p>` 元素 
定义了HTML文档中的一个段落

### (2) `body>`元素
定义了HTML文档的主体

### (3) `< html>`元素
定义了整个HTML文档

<br/>

另:

* 空的HTML元素,如`<br/>`
* HTML对大小写不敏感,但推荐使用小写

<br/>

# 三, HTML 属性

* HTML 标签可以拥有属性。属性提供了有关 HTML 元素的更多的信息
* 属性总是以名称/值对的形式出现，比如：name="value"
* 属性总是在 HTML 元素的开始标签中规定

### (1)属性-链接地址
HTML 链接由 `<a>` 标签定义。链接的地址在 `href` 属性中指定
```html
<a href="http://www.w3school.com.cn">This is a link</a>
```

### (2)属性-居中排列
`<h1>` 定义标题的开始。
```html
<h1 align="center"> 
```
表示 居中排列标题

### (3)属性-背景颜色
`<body>` 定义 HTML 文档的主体。
```html
<body bgcolor="yellow">
``` 
表示 背景颜色


另: 
* 属性值应该始终被包括在引号内。 **双引号**是最常用的
* 属性值本身就含有双引号，则必须使用单引号

<br/>

# 四, HTML 标题

### (1) HTML 标题
标题（Heading）是通过 `<h1> - <h6>`等标签进行定义的。

* `<h1>` 定义最大的标题
* `<h6>` 定义最小的标题
* 不要仅仅是为了产生粗体或大号的文本而使用标题

### (2) HTML 水平线

* `<hr /> `标签在 HTML 页面中创建水平线。
* hr 元素可用于分隔内容。

### (3) HTML 注释
```html
<!-- This is a comment -->
```

<br/>

# 五, HTML 段落
> 没啥好说的

<br/>


# 六, HTML 样式

style 属性用于改变 HTML 元素的样式

样式是 HTML 4 引入的，它是一种新的首选的改变 HTML 元素样式的方式。通过 HTML 样式，能够通过使用 style 属性直接将样式添加到 HTML 元素，或者间接地在独立的样式表中（CSS 文件）进行定义

* background-color 属性定义了 背景颜色
* font-family 属性定义元素中文本的 字体系列
* color 属性定义元素中文本的 颜色
* font-size 属性定义元素中文本的 字体尺寸
* text-align 属性规定了元素中文本的 水平对齐方式


<br/>

# 七, HTML格式化


* 文本格式化, 有很多.
* `<pre>`标签适合显示计算机代码
* 缩写和首字母缩写(在某些浏览器中，当您把鼠标移至缩略词语上时，title 可用于展示表达的完整版本)
* 引用: `<blockquote>` 用于长引用,`<q>`用于短引用
* `<del>` 显示删除线
* `<ins>` 显示下划线

<br/>

# 八, HTML引用

* 引用: `<blockquote>` 用于长引用,`<q>`用于短引用    
* 缩略词 `<abbr>`
* HTML `<dfn>`元素定义项目或缩写的定义(目前看来和`<abbr>`类似)
* HTML `<address>` 元素定义文档或文章的联系信息, 此元素通常以斜体显示
* HTML `<cite>` 元素定义著作的标题
* `<bdo>`定义文本方向

<br/>

# 九, HTML计算机代码元素

* HTML `<kbd>` 元素定义键盘输入
* HTML `<samp>` 元素定义计算机输出
* HTML `<code>` 元素定义编程代码
* `<code>` 元素不保留多余的空格和折行,如需解决该问题，必须在 `<pre>` 元素中包围代码
* HTML `<var>` 元素定义数学变量


<br/>

# 十, HTML注释
* 注释标签 `<!-- 与 -->` 用于在 HTML 插入注释


<br/>

# 十一, HTML CSS

### (1) 外部样式表
当样式需要被应用到很多页面的时候，外部样式表将是理想的选择。使用外部样式表，就可以通过更改一个文件来改变整个站点的外观。
> 用外部文件定义整个文件的格式


### (2) 内部样式表
当单个文件需要特别样式时，就可以使用内部样式表。可以在 head 部分通过 `<style>` 标签定义内部样式表
> 在 head部分定义整个文件的格式

### (3) 内联样式
当特殊的样式需要应用到个别元素时，就可以使用内联样式。 使用内联样式的方法是在相关的标签中使用样式属性。样式属性可以包含任何 CSS 属性
> 在部分区域定义该区域的格式


<br/>

# 十二, HTML 链接

* 通过链接可以指向 本站点的某个目录 或 一个网址 
* 也可以将图片作为链接
* 通过使用 `<a>` 标签在 HTML 中创建链接(通过使用 href 属性 - 创建指向另一个文档的链接
通过使用 name 属性 - 创建文档内的书签)
* HTML 链接语法 `<a href="url">Link text</a>`
* 把链接的 target 属性设置为 `"_blank"`, 该链接会在一个新的窗口中打开
* 邮件链接`<a href="mailto:ruilin1024@outlook.com"></a>`,这样写就足矣.

### (1) HTML 链接 - name 属性

name 属性规定锚（anchor）的名称。 
> 什么是锚呢, 我个人的理解就是放一个链接指向同一个文件的另一个地方.

* 对锚进行命名（创建一个书签）
`<a name="tips">基本的注意事项 - 有用的提示</a>`

* 创建指向该锚的链接：
`<a href="#tips">有用的提示</a>`

* 也可以在其他页面中创建指向该锚的链接：
`<a href="http://www.w3school.com.cn/html/html_links.asp#tips">有用的提示</a>`
 `URL`+ `#` + `锚名称`


### (2) 关于写链接的时候是否要在URL末尾添加正斜杠:
* 当URL后不加斜杠指向的是网站目录下的一个文件，而加了反斜杠则表示指向的是一个目录，也就是目录与文件的区别。
* 在写HTML 里面的链接时, 如果 URL 末尾没有添加正斜杠,客户端就会向服务器产生两次 HTTP 请求。这是因为服务器会添加正斜杠到这个地址，然后创建一个新的请求.

<br/>

# 十三, HTML 图像

### (1) 图像标签(`<img>`)和源属性(`Src`)
```html
<img src="url" />
```

### (2)  替换文本属性(`Alt`)
在浏览器无法载入图像时，替换文本属性告诉读者它们失去的信息。此时，浏览器将显示这个替代性的文本而不是图像。
```html
<img src="boat.gif" alt="Big Boat">
```

<br/>

# 十四, HTML 表格

* 每个表格由 `table` 标签开始。
* 每个表格行由 `tr` 标签开始。
* 每个表格数据由 `td` 标签开始。
* `border` 属性规定规定围绕表格的边框的宽度
* 表格的表头使用 `<th>` 标签进行定义


<br/>

# 十五, HTML 列表

### (1) 无序列表
无序列表始于 `<ul>` 标签。每个列表项始于 `<li>`
```html
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>
```

### (2) 有序列表
有序列表始于 `<ol>` 标签。每个列表项始于 `<li>` 标签
```html
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
```

### (3) 定义列表

* 自定义列表以 `<dl>` 标签开始。每个自定义列表项以 `<dt>` 开始。每个自定义列表项的定义以 `<dd>` 开始。
* 自定义列表不仅仅是一列项目，而是项目及其注释的组合.

<br/>

# 十六, HTML 块
> division 读法 美`[dɪˈvɪʒən]`

HTML `<div>` 和 `<span>`
### (1) HTML 块元素  (block level element)
* 大多数 HTML 元素被定义为块级元素或内联元素。
* 块级元素在浏览器显示时，通常会以新行来开始（和结束）。
* 例子：`<h1>`, `<p>`, `<ul>`, `<table>`

### (2) HTML 内联元素 (inline element)
内联元素在显示时通常不会以新行开始。
例子：`<b>`, `<td>`, `<a>`, `<img>`

### (3) HTML `<div>` 元素
* HTML `<div>` 元素是块级元素，它是可用于组合其他 HTML 元素的容器。
* 定义文档中的分区或节（division/section）

### (4) HTML `<span>` 元素
* HTML `<span>` 元素是内联元素，可用作文本的容器。
* 定义 span，用来组合文档中的行内元素。

<br/>

# 十七, HTML 类
定义一个 `<div>` 元素的类, 或定义一个`<span>`元素的类。以便在其他地方直接利用

<br/>

# 十八， HTML 布局
> 飘过.....

<br/>

# 十九, HTML 响应式 Web 设计

### (1) 创建自己的响应式设计
创建响应式设计的一个方法，是自己来创建它

### (2) 使用 Bootstrap
* 另一个创建响应式设计的方法，是使用现成的 CSS 框架。
* Bootstrap 是最流行的开发响应式 web 的 HTML, CSS, 和 JS 框架。
>CSS还没看....

<br/>

# 二十, HTML 框架

* 通过使用框架，可以在同一个浏览器窗口中显示不止一个页面。
* 每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。

### (1) 框架结构标签（`<frameset>`）
* 框架结构标签（`<frameset>`）定义如何将窗口分割为框架
* 每个 frameset 定义了一系列行或列
* rows/columns 的值规定了每行或每列占据屏幕的面积

### (2) 框架标签（Frame）
Frame 标签定义了放置在每个框架中的 HTML 文档。

在下面的这个例子中，我们设置了一个两列的框架集。第一列被设置为占据浏览器窗口的 25%。第二列被设置为占据浏览器窗口的 75%。HTML 文档 "frame_a.htm" 被置于第一个列中，而 HTML 文档 "frame_b.htm" 被置于第二个列中：
```html
<frameset cols="25%,75%">
   <frame src="frame_a.htm">
   <frame src="frame_b.htm">
</frameset>
```

<br/>

# 二十一, HTML 内联框架

### (1) 添加 iframe 的语法

```html
<iframe src="URL"></iframe>
```

URL 指向隔离页面的位置。

### (2) Iframe - 设置高度和宽度
* height 和 width 属性用于规定 iframe 的高度和宽度。
* 属性值的默认单位是像素，但也可以用百分比来设定(比如 "80%")

```html
<iframe src="demo_iframe.htm" width="200" height="200"></iframe>
```

### (3) Iframe - 删除边框
* frameborder 属性规定是否显示 iframe 周围的边框。
* 设置属性值为 "0" 就可以移除边框：

```html
<iframe src="demo_iframe.htm" frameborder="0"></iframe>
```

### (4) 使用 iframe 作为链接的目标
* iframe 可用作链接的目标 (target)
* 链接的 target 属性必须引用 iframe 的 name 属性：

```html
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>
<p><a href="http://www.w3school.com.cn" target="iframe_a">W3School.com.cn</a></p>
```

>由于链接 (https://w3school.com.cn) 的目标 (W3School.com.cn) 匹配 iframe 的名称，所以链接会在 iframe 中打开 (即在小框内打开对应的网页)

<br/>

# 二十二, HTML 背景

背景 (Backgrounds) `<body>` 拥有两个配置背景的标签。背景可以是颜色或者图像。

### (1) 背景颜色 (Bgcolor)
背景颜色属性将背景设置为某种颜色

```html
<body bgcolor="#000000">
```

### (2) 背景 (Background)
* 背景属性将背景设置为图像。属性值为图像的URL。
* URL可以是相对地址(/home/1.jpg), 也可以是绝对地址(https://...)

```html
<body background="clouds.gif">
<body background="http://www.w3school.com.cn/clouds.gif">
```

<br/>

# 二十三, HTML 脚本

### (1) HTML script 元素
* `<script>` 标签用于定义客户端脚本, 比如 JavaScript。
* script 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。
* 必需的 type 属性规定脚本的 MIME 类型。
* JavaScript 最常用于图片操作、表单验证以及内容动态更新。

> 注:  MIME(Multipurpose Internet Mail Extensions)多用途互联网邮件扩展类型。是设定某种扩展名的文件用一种应用程序来打开的方式类型，当该扩展名文件被访问的时候，浏览器会自动使用指定应用程序来打开。常见的MIME 类型有 .gif .avi .gz等.

### (2) `<noscript>` 标签
* `<noscript>` 标签提供无法使用脚本时的替代内容，比方在浏览器禁用脚本时，或浏览器不支持客户端脚本时。
* 只有在浏览器不支持脚本或者禁用脚本时，才会显示 noscript 元素中的内容


### (3) 如何应付老式的浏览器
* 如果浏览器压根没法识别 `<script>` 标签，那么 `<script>` 标签所包含的内容将以文本方式显示在页面上。
* 为了避免这种情况发生，应该将脚本隐藏在注释标签当中。那些老的浏览器（无法识别 `<script>` 标签的浏览器）将忽略这些注释，所以不会将标签的内容显示到页面上。
* 而那些新的浏览器将读懂这些脚本并 **执行** 它们, **即使代码被嵌套** 在注释标签内。

```js
<script type="text/javascript">
<!--
document.write("Hello World!")
//-->
</script>
```

<br/>

# 二十四, HTML 头部

### (1) HTML `<head>`元素
`<head>` 元素是所有头部元素的容器

### (2) HTML `<title>` 元素
* `<title>` 标签定义文档的标题
* `<title>` 内的内容不再页面中显示

### (3) HTML `<base>` 元素
`<base>` 标签为页面上的所有链接规定默认地址或默认目标(target)
```html
<head>
<base href="http://www.w3school.com.cn/images/" />
<base target="_blank" />
</head>
```

### (4) HTML `<link>` 元素
* `<link>`标签定义文档与外部资源之间的关系
* `<link>`标签最常用于连接样式表：
```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

### (5) HTML `<style>` 元素
* `<style>` 标签用于为 HTML 文档定义样式信息。
* 可以在 style 元素内规定 HTML 元素在浏览器中呈现的样式：

```html
<head>
<style type="text/css">
body {background-color:yellow}
p {color:blue}
</style>
</head>
```

### (6) HTML `<meta>` 元素
* 元数据(metadata) 是关于数据的信息。
* `<meta>` 标签提供关于 HTML 文档的元数据。元数据不会显示在页面上，但是对于机器是可读的.
* 典型的情况是，meta 元素被用于规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据。
* 一些搜索引擎会利用 meta 元素的 name 和 content 属性来索引页面.

```html
<meta name="description" content="Free Web tutorials on HTML, CSS, XML" />
```

### (7) HTML `<script>` 元素
`<script>` 标签用于定义客户端脚本，比如 JavaScript。

<br/>

# 二十五, HTML 实体

HTML 字符实体

* 在 HTML 中，某些字符是预留的。
* 在 HTML 中不能使用小于号 `<` 和大于号 `>`，这是因为浏览器会误认为它们是标签。
* 如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体(character entities).


如需显示小于号，必须这样写：`&lt;` 或 `&#60;`

具体的实体字符可以 百度 "[HTML 实体符号参考手册](http://www.w3school.com.cn/tags/html_ref_entities.html)".

<br/>

# 二十六, HTML URL
URL (Uniform Resource Locator), 中文也译为"统一资源定位符"
* URL 也被称为网址
* URL 可以是域名, 或者是IP地址.

### (1) URL
网址，比如 `http://www.w3school.com.cn/html/index.asp`, 遵守以下的语法规则：

`scheme://host.domain:port/path/filename`

解释：
* `scheme` - 定义因特网服务的类型。最常见的类型是 http
* `host` - 定义域主机（http 的默认主机是 www）
* `domain` - 定义因特网域名，比如 w3school.com.cn
* `:port` - 定义主机上的端口号（http 的默认端口号是 80）
* `path` - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
* `filename` - 定义文档/资源的名称

### (2) URL Schemes
常见的如下:

* http
* https
* ftp
* file

<br/>

# 二十七, HTML URL 字符编码

URL 编码会将字符转换为可通过因特网传输的格式

* URL 只能使用 ASCII 字符集来通过因特网进行发送。
* 由于 URL 常常会包含 ASCII 集合之外的字符，URL 必须转换为有效的 ASCII 格式。
* URL 编码使用 "%" 其后跟随两位的十六进制数来替换非 ASCII 字符。
* URL 不能包含空格。URL 编码通常使用 + 来替换空格。

<br/>

# 二十八, HTML Web Server

过.

<br/>

# 二十九, HTML 颜色

### (1) 颜色值
* 颜色由一个十六进制符号来定义(Color HEX), 这个符号由红色、绿色和蓝色的值组成(Color RGB)
* 每种颜色的最小值是0(十六进制：#00), 最大值是255 (十六进制：#FF) 

### (2) 颜色名
* 大多数的浏览器都支持颜色名集
* 仅仅有 16 种颜色名被 W3C 的 HTML4.0 标准所支持
* 如果需要使用其它的颜色，需要使用十六进制的颜色值

### (3) Web安全色
数年以前，当大多数计算机仅支持 256 种颜色的时候，一系列 216 种 Web 安全色作为 Web 标准被建议使用。其中的原因是，微软和 Mac 操作系统使用了 40 种不同的保留的固定系统颜色 (双方大约各使用 20 种)

不过越来越多的计算机有能力处理数百万种颜色, 这样做的意义不是很大.

<br/>

#  三十, HTML 颜色名

过..

<br/>

# 三十一, HTML 文档类型

`<!DOCTYPE>`声明帮助浏览器正确地显示网页

`<!DOCTYPE>`不是 HTML 标签。它为浏览器提供一项信息（声明），即 HTML 是用什么版本编写的, 以便浏览器正确的显示 HTML 文件

* HTML5 的声明:
```html
<!DOCTYPE html>
```
* 而 HTML 4.01 和 HTML 1.0 等版本的声明都是不同的.

<br/> 

# 三十二, HTML 速查手册

[参考W3School](http://www.w3school.com.cn/html/html_quick.asp)


