---
layout: post
title: "JavaScript-Stuying"
date: 2019-04-04
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> 从4.3号下午开始看, 一直看到现在--4.4号凌晨两点. 我该睡了...头发要紧...

[参考菜鸟教程](http://www.runoob.com/js/js-intro.html)


# 一. JS 简介
### (1) 直接写入HTML输入流
```js
document.write("<h1>这是一个标题</h1>");
document.write("<p>这是一个段落。</p>");
```

### (2) 对事件的反应
```js
<button type="button" onclick="alert('欢迎!')">点我!</button>
```

### (3) 改变HTML内容
```js
x=document.getElementById("demo");  //查找元素
x.innerHTML="Hello JavaScript";    //改变内容
```

### (4) 改变HTML图像
实例中代码 element.src.match("bulbon") 的作用意思是：检索 `<img id="myimage" onclick="changeImage()" src="/images/pic_bulboff.gif" width="100" height="180">` 里面 src 属性的值有没有包含 bulbon 这个字符串，如果存在字符串 bulbon，图片 src 更新为 bulboff.gif，若匹配不到 bulbon 字符串，src 则更新为 bulbon.gif
```js
<script>
function changeImage()
{
    element=document.getElementById('myimage')
    if (element.src.match("bulbon"))
    {
        element.src="/images/pic_bulboff.gif";
    }
    else
    {
        element.src="/images/pic_bulbon.gif";
    }
}
</script>
<img id="myimage" onclick="changeImage()" src="/images/pic_bulboff.gif" width="100" height="180">
```

### (5) 改变 HTML 样式
```js
x=document.getElementById("demo")  //找到元素 
x.style.color="#ff0000";           //改变样式
```

### (6) 验证输入
```js
if isNaN(x) {
    alert("不是数字");
}
```
更严格的判断需要用到正则表达式:
```js
if(isNaN(x)||x.replace(/(^\s*)|(\s*$)/g,"")==""){
    alert("不是数字");
}
```

<br/>

# 二. JS 用法

### (1) `<script>`和`<body>`标签
HTML 中的脚本必须位于 `<script>` 与 `</script>` 标签之间。

脚本可被放置在 HTML 页面的 `<body>` 和 `<head>` 部分中

### (2) 在 `<head>` 或者 `<body>` 的JavaScript
通常的做法是把函数放入 `<head>` 部分中，或者放在页面底部。这样就可以把它们安置到同一处位置，不会干扰页面的内容。

### (3) 外部的 JavaScript
也可以把脚本保存到外部文件中。外部文件通常包含被多个网页使用的代码。

如需使用外部文件，请在 `<script>` 标签的 "src" 属性中设置该 .js 文件：
```js
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>
```

<br/>

# 三. JS 输出
### (1) JavaScript 显示数据
JavaScript 可以通过不同的方式来输出数据：
* 使用 window.alert() 弹出警告框。
* 使用 document.write() 方法将内容写到 HTML 文档中。
* 使用 innerHTML 写入到 HTML 元素。
* 使用 console.log() 写入到浏览器的控制台。

### (2) 使用 window.alert()
弹出警告框来显示数据：
```js
<script>
window.alert(5 + 6);
</script>
```


### (3) 操作HTML元素
* 使用 "id" 属性来标识 HTML 元素
* document.getElementById("demo") 是使用 id 属性来查找 HTML 元素的 JavaScript 代码 。
* innerHTML = "段落已修改。" 是用于修改元素的 HTML 内容(innerHTML)的 JavaScript 代码。

```js
<p id="demo">我的第一个段落</p>

<script>
document.getElementById("demo").innerHTML = "段落已修改。";
</script>
```

### (4) 写到HTML文档
```js
<script>
document.write(Date());
</script>
```
注意: 如果在文档已完成加载后执行 document.write，整个 HTML 页面将被覆盖。
例如, 下面的代码中页面已经加载完成, 点击按钮,执行document.write,此时写入的内容会覆盖整个页面
```js
<p>我的第一个段落。</p>

<button onclick="myFunction()">点我</button>

<script>
function myFunction() {
   	document.write(Date());
}
</script>
```

### (5) 写到控制台
使用 console.log() 方法在浏览器的控制台中显示 JavaScript 值。
```js
<script>
a = 5;
b = 6;
c = a + b;
console.log(c);
</script>
```

<br/>

# 四. JS 语法
### (1) JS 字面量
#### 1. 数字

#### 2. 字符串
字符串字面量可以使用单引号或双引号

#### 3. 表达式

#### 4. 数组(Array)
```js
[40, 100, 1, 5, 25, 10]
```

#### 5. 对象
```js
{firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"}
```
#### 6. 函数
```js
function myFunction(a, b) { return a * b;}
```

### (2) JS 变量
JS使用关键字`var`来定义变量
```js
var x, length

x = 5

length = 6
```

### (3) JS操作符
> 貌似和其他的语言没什么不同

### (4) JS语句
JS语句用分号分隔

### (5) JS 关键字
JS保留了一些关键字为自己所用

var关键字告诉浏览器创建一个新的变量

### (6) JS 注释
JS注释为双斜杠

### (7) JS 数据类型
JavaScript 有多种数据类型：数字，字符串，数组，对象等等：
```js
var length = 16;                                  // Number 通过数字字面量赋值 
var points = x * 10;                              // Number 通过表达式字面量赋值
var lastName = "Johnson";                         // String 通过字符串字面量赋值
var cars = ["Saab", "Volvo", "BMW"];              // Array  通过数组字面量赋值
var person = {firstName:"John", lastName:"Doe"};  // Object 通过对象字面量赋值
```
### (8) JS 函数
```js
function myFunction(a, b) {
   	return a * b;                                // 返回 a 乘以 b 的结果
}
```

### (9) JavaScript 字母大小写
JavaScript 对大小写是敏感的

### (10) JavaScript 字符集
JavaScript 使用 Unicode 字符集。

Unicode 覆盖了所有的字符，包含标点等字符。

<br/>

# 五. JS 语句

JavaScript 语句向浏览器发出的命令。语句的作用是告诉浏览器该做什么。

### (1) 对代码行进行折行
可以在文本字符串中使用反斜杠对代码行进行换行
```js
document.write("你好 \
世界!");
```
>  其他的貌似和其他语言一样

<br/>

# 六. JS 注释
* 单行注释`//`
* 多行注释`/**/`
* 行末也可以注释

<br/>

# 七. JS 变量
### (1) JS 变量
*  变量必须以字母开头
*  不推荐变量使用`$`和`_`开头

### (2) 声明(创建)JS变量
一个好的编程习惯是，在代码开始处，统一对需要的变量进行声明。

<br/>

# 八. JS 数据类型
### (1) JS拥有动态类型
JavaScript 拥有动态类型。这意味着相同的变量可用作不同的类型：
```js
var x;               // x 为 undefined
var x = 5;           // 现在 x 为数字
var x = "John";      // 现在 x 为字符串
```

### (2) JS 布尔
布尔（逻辑）只能有两个值：true 或 false。
```js
var x=true;
var y=false;
```
### (3) JS 数组
下面的代码创建名为 cars 的数组：
```js
var cars=new Array();
cars[0]="Saab";
cars[1]="Volvo";
cars[2]="BMW";
```
或者 压缩数组 (condensed array):
```js
var cars=new Array("Saab","Volvo","BMW");
```
或者 字面数组(literal array):
```js
var cars=["Saab","Volvo","BMW"];
```

### (4) JS 对象
定义:
```js
var person={
firstname : "John",
lastname  : "Doe",
id        :  5566
};
```
使用:(下面两行代码表达的效果是一样的)
```js
name=person.lastname;
name=person["lastname"];
```

### (5) Undefined 和 Null
Undefined 这个值表示变量不含有值。

可以通过将变量的值设置为 null 来清空变量。
```js
cars=null;
person=null;
```

### (6) 声明变量类型
当声明新变量时，可以使用关键词 "new" 来声明其类型：
```js
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;
```

> JavaScript 变量均为对象。当声明一个变量时，就创建了一个新的对象。


<br/>

# 九. JS对象

### (1) 对象属性
* "JavaScript 对象是变量的容器"。
* 通常认为 "JavaScript 对象是键值对的容器"。
* 键值对通常写法为 `name : value` (键与值以冒号分割)。
* 键值对在 JavaScript 对象通常称为 对象属性。

### (2) 访问对象属性
两种方法访问对象属性
```js
person.lastName;

person["lastName"];
```

### (3) 对象方法

#### 定义:
```js
var person = {
    firstName: "John",
    lastName : "Doe",
    fullName : function() 
	{
       return this.firstName + " " + this.lastName;
    }
};
```
#### 访问:
访问对象的方法(函数)运行结果:
```js
name = person.fullName(); //即返回运行结果John Doe
```
访问对象方法(函数)的属性:
```js
name = person.fullName; //即返回return this.firstname +........
```
> 通常 fullName() 是作为 person 对象的一个方法， fullName 是作为一个属性。

<br/>

# 十. JS函数

### (1) 局部 JS 变量
在JS函数内部声明的变量是局部变量, 所以只能在函数内部访问它

### (2) 全局 Js 变量
在函数外声明的变量是全局变量, 网页上的所有脚本和函数都能访问它

<br/>

# 十一. JS 作用域

> 飘过

<br/>

# 十二. JS 事件

### (1) HTML 事件
HTML 事件可以是浏览器行为，也可以是用户行为。

以下是 HTML 事件的实例：
* HTML 页面完成加载
* HTML input 字段改变时
* HTML 按钮被点击

### (2) 显示时间
* 通过修改id="demo"元素的内容来修改
* 代码修改自身元素的内容
```js
<button onclick="this.innerHTML=Date()">现在的时间是?</button>
```
* 调用函数来修改

### (3) 常见的HTML事件
* onchange	HTML 元素改变
* onclick	用户点击 HTML 元素
* onmouseover	用户在一个HTML元素上移动鼠标
* onmouseout	用户从一个HTML元素上移开鼠标
* onkeydown	   用户按下键盘按键
* onload	 浏览器已完成页面的加载

<br/>

# 十三. JS 字符串
### (1) 字符串
在字符串里面添加转义字符来使用引号:
```js
var x = 'It\'s alright';
```

### (2) 字符串长度
可以使用内置属性 length 来计算字符串的长度：
```js
var txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
var sln = txt.length;
```

### (3) 字符串可以是对象
> 但是,不要创建 String 对象。它会拖慢执行速度，并可能产生其他副作用：


```js
var x = "John";
var y = new String("John");
typeof x // 返回 String
typeof y // 返回 Object
```

<br/>

# 十四. JS 运算符
### (1) 对字符串和数字进行加法运算
两个数字相加，返回数字相加的和，如果数字与字符串相加，返回字符串，如下实例：
```js
x=5+5;
y="5"+5;
z="Hello"+5;
```
x,y, 和 z 输出结果为:
```js
10
55
Hello5
```
> 规则:如果把数字与字符串相加，结果将成为字符串


<br/>

# 十五. JS 比较
### (1) 比较运算符
* `==`为等于
* `===`为绝对等于(值和类型均相等)
* `!=`不等于
* `!==`不绝对等于(值和类型有一个不相等，或两个都不相等)

### (2) 条件运算符
JavaScript 还包含了基于某些条件对变量进行赋值的条件运算符。
```js
variablename=(condition)?value1:value2 
```

<br/>

# 十六. JS 条件语句
> if else之类的...

<br/>

# 十七. JS switch 语句
使用 default 关键词来规定匹配不存在时做的事情
```js
switch (d)
{
    case 6:x="今天是星期六";
    break;
    case 0:x="今天是星期日";
    break;
    default:
    x="期待周末";
}
```
<br/>

# 十八. JS 循环
### (1) 循环
for 循环
```js
for (var i=0;i<cars.length;i++)
{ 
    document.write(cars[i] + "<br>");
}
```

### (2) For/In循环

### (3) JavaScript for/in 语句循环遍历对象的属性：
```js
var person={fname:"John",lname:"Doe",age:25}; 
 
for (x in person)  // x 为属性名
{
    txt=txt + person[x];
}
```
得到的结果为:
```js
BillGates56
```

<br/>

# 十九. while 循环
### (1) do/while循环
* 该循环会在检查条件是否为真之前执行一次代码块，然后如果条件为真的话，就会重复这个循环。
* 也就是说不管条件正不正确, 都会先执行一次do{}.

<br/>

# 二十. JS Break 和 Continue 语句
### (1) Break 语句
> break 语句直接跳出 for 循环

### (2) Continue 语句
中断循环中的迭代,直接去 判断条件那儿

### (3) JavaScript 标签
标记 JavaScript 语句，在语句之前加上冒号：
```js
label:
statements
```
通过标签使用,break语句可用于跳出任何JS代码块:
```js
cars=["BMW","Volvo","Saab","Ford"];
list: 
{
    document.write(cars[0] + "<br>"); 
    break list;
    document.write(cars[3] + "<br>"); 
}
```

<br/>

# 二十一. JS typeof

### (1) typeof 操作符
使用 typeof 操作符来检测变量的数据类型。
```js
typeof "John"                // 返回 string 
typeof 3.14                  // 返回 number
typeof false                 // 返回 boolean
typeof [1,2,3,4]             // 返回 object
typeof {name:'John', age:34} // 返回 object
```
> 在JavaScript中，数组是一种特殊的对象类型。 因此 `typeof [1,2,3,4]`返回 object。 

### (2) undefined 和 null 的区别
```js
var person = null;           
var person = undefined;     
```

null 和 undefined 的值相等，但类型不等：
```js
typeof undefined             // undefined
typeof null                  // object
null === undefined           // false
null == undefined            // true
```

<br/>

# 二十二. JavaScript 类型转换
### (1) JavaScript 数据类型
在 JavaScript 中有 5 种不同的数据类型：
* string
* number
* boolean
* object
* function


3 种对象类型：
* Object
* Date
* Array

2 个不包含任何值的数据类型：
* null
* undefined

### (2) typeof 操作符
使用 typeof 操作符来查看 JavaScript 变量的数据类型。
```js
typeof "John"                 // 返回 string 
typeof 3.14                   // 返回 number
typeof NaN                    // 返回 number
typeof false                  // 返回 boolean
typeof [1,2,3,4]              // 返回 object
typeof {name:'John', age:34}  // 返回 object
typeof new Date()             // 返回 object
typeof function () {}         // 返回 function
typeof myCar                  // 返回 undefined (如果 myCar 没有声明)
typeof null                   // 返回 object
```

> NaN (Not a Number，非数)

* NaN 的数据类型是 number
* 数组(Array)的数据类型是 object
* 日期(Date)的数据类型为 object
* null 的数据类型是 object
* 未定义变量的数据类型为 undefined


### (3) constructor 属性
constructor 属性返回所有 JavaScript 变量的构造函数。
```js
"John".constructor                 // 返回函数 String()  { [native code] }
(3.14).constructor                 // 返回函数 Number()  { [native code] }
false.constructor                  // 返回函数 Boolean() { [native code] }
[1,2,3,4].constructor              // 返回函数 Array()   { [native code] }
{name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
new Date().constructor             // 返回函数 Date()    { [native code] }
function () {}.constructor         // 返回函数 Function(){ [native code] }
```

### (4) 将数字转换为字符串
全局方法 String() 可以将数字转换为字符串。
```js
String(x)         // 将变量 x 转换为字符串并返回
String(123)       // 将数字 123 转换为字符串并返回
```

Number 方法 toString() 也是有同样的效果。
```js
x.toString()
(123).toString()
(100 + 23).toString()
```

### (5) 将布尔值转换为字符串
全局方法 String() 可以将布尔值转换为字符串。
```js
String(false)        // 返回 "false"
String(true)         // 返回 "true"
```

Boolean 方法 toString() 也有相同的效果。
```js
false.toString()     // 返回 "false"
true.toString()      // 返回 "true"
```

### (6) 将日期转换为字符串
> 类似

### (7) 将字符串转换为数字
全局方法 Number() 可以将字符串转换为数字。

* 字符串包含数字(如 "3.14") 转换为数字 (如 3.14).
* 空字符串转换为 0。
* 其他的字符串会转换为 NaN (不是个数字)。
```js
Number("3.14")    // 返回 3.14
Number(" ")       // 返回 0 
Number("")        // 返回 0
Number("99 88")   // 返回 NaN
```
另外: 
* parseFloat()	解析一个字符串，并返回一个浮点数。
* parseInt()	解析一个字符串，并返回一个整数。

### (8) 一元运算符 +
Operator + 可用于将变量转换为数字：
```js
var y = "5";      // y 是一个字符串
var x = + y;      // x 是一个数字
```

如果变量不能转换，它仍然会是一个数字，但值为 NaN (不是一个数字):
> 有点绕, 想想就能想通.他是数字类型,但是值为NaN.而NaN的意思是不是一个数字.


```js
var y = "John";   // y 是一个字符串
var x = + y;      // x 是一个数字 (NaN)
```

### (9) 将布尔值转换为数字
全局方法 Number() 可将布尔值转换为数字。
```js
Number(false)     // 返回 0
Number(true)      // 返回 1
```

### (10) 将日期转换为数字
全局方法 Number() 可将日期转换为数字。
```js
d = new Date();
Number(d)          // 返回 1404568027739
```
日期方法 getTime() 也有相同的效果。
```js
d = new Date();
d.getTime()        // 返回 1404568027739
```

### (11) 自动转换类型
当 JavaScript 尝试操作一个 "错误" 的数据类型时，会自动转换为 "正确" 的数据类型。
> 这些结果看看就行了....


```js
5 + null    // 返回 5         null 转换为 0
"5" + null  // 返回"5null"   null 转换为 "null"
"5" + 1     // 返回 "51"      1 转换为 "1"  
"5" - 1     // 返回 4         "5" 转换为 5
```

### (12) 自动转换为字符串
当尝试输出一个对象或一个变量时 JavaScript 会自动调用变量的 toString() 方法：
```js
document.getElementById("demo").innerHTML = myVar;

myVar = {name:"Fjohn"}  // toString 转换为 "[object Object]"
myVar = [1,2,3,4]       // toString 转换为 "1,2,3,4"
myVar = new Date()      // toString 转换为 "Fri Jul 18 2014 09:08:55 GMT+0200"
```
数字和布尔值也经常相互转换：
```js
myVar = 123             // toString 转换为 "123"
myVar = true            // toString 转换为 "true"
myVar = false           // toString 转换为 "false"
```

<br/>

# 二十三. JS 正则表达式

### (1) 正则表达式
* 正则表达式是由一个字符序列形成的搜索模式。
* 当你在文本中搜索数据时，你可以用搜索模式来描述你要查询的内容。
* 正则表达式可以是一个简单的字符，或一个更复杂的模式。
* 正则表达式可用于所有文本搜索和文本替换的操作。

#### 语法:
* /正则表达式主体/修饰符(可选)
* 其中修饰符是可选的。
```js
var patt = /runoob/i
```
* /runoob/i  是一个正则表达式。
* runoob  是一个正则表达式主体 (用于检索)。
* i  是一个修饰符 (搜索不区分大小写)。


### (2) search() 方法使用正则表达式
使用正则表达式搜索 "Runoob" 字符串，且不区分大小写：
```js
var str = "Visit Runoob!"; 
var n = str.search(/Runoob/i);
```
输出结果为：
```js
6
```
> 6表示 Runoob! 一共有7个字符, 0~6


### (3) search() 方法使用字符串
search 方法可使用字符串作为参数。字符串参数会转换为正则表达式：
`
检索字符串中 "Runoob" 的子串：
```js
var str = "Visit Runoob!"; 
var n = str.search("Runoob");
```


### (4) replace() 方法使用正则表达式
使用正则表达式且不区分大小写将字符串中的 Microsoft 替换为 Runoob :
```js
var str = document.getElementById("demo").innerHTML; 
var txt = str.replace(/microsoft/i,"Runoob");
```
结果输出为:
```js
Visit Runoob!
```
### (5) replace() 方法使用字符串
replace() 方法将接收字符串作为参数：
```js
var str = document.getElementById("demo").innerHTML; 
var txt = str.replace("Microsoft","Runoob");
```


### (6) 正则表达式修饰符
### (7) 正则表达式模式
> 这两个比较杂, 用的时候再百度吧.


### (8) 使用 RegExp 对象
在 JavaScript 中，RegExp 对象是一个预定义了属性和方法的正则表达式对象。

### (9) 使用 test()
test() 方法是一个正则表达式方法。

test() 方法用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。
```js
var patt = /e/;
patt.test("The best things in life are free!");
```
字符串中含有 "e"，所以该实例输出为：
```js
ture
```

也可以不用设置正则表达式的变量，以上两行代码可以合并为一行：
```js
/e/.test("The best things in life are free!")
```


### (10) 使用 exec()
exec() 方法是一个正则表达式方法。

exec() 方法用于检索字符串中的正则表达式的匹配。

**该函数返回一个数组**，其中存放匹配的结果。如果未找到匹配，则返回值为 null。
```js
Example 1
/e/.exec("The best things in life are free!");
```
字符串中含有 "e"，所以该实例输出为:
```js
e
```

<br/>

# 二十五. JS 错误
* try 语句测试代码块的错误。
* catch 语句处理错误。
* throw 语句创建自定义错误。
* finally 语句在 try 和 catch 语句之后，无论是否有触发异常，该语句都会执行。


### (1) JS try 和 catch
> 运行try里面的内容.如果失败,catch到err,输出错误信息


```js
var txt=""; 
function message() 
{ 
    try { 
        adddlert("Welcome guest!"); 
    } catch(err) { 
        txt="本页有一个错误。\n\n"; 
        txt+="错误描述：" + err.message + "\n\n"; 
        txt+="点击确定继续。\n\n"; 
        alert(txt); 
    } 
}
```

### (2) finally 语句
finally 语句不论之前的 try 和 catch 中是否产生异常都会执行该代码块。

### (3) Throw 语句
throw 语句允许我们创建自定义错误。

正确的技术术语是：创建或抛出异常（exception）
```js
    try { 
        if(x == "")  throw "值为空";
        if(isNaN(x)) throw "不是数字";
        x = Number(x);
        if(x < 5)    throw "太小";
        if(x > 10)   throw "太大";
    }
 ```

<br/>

# 二十六. JS 调试

### (1) console.log() 方法
如果浏览器支持调试，可以使用 console.log() 方法在调试窗口上打印 JavaScript 值：
```js
a = 5;
b = 6;
c = a + b;
console.log(c);
```

### (2) debugger 关键字
* debugger 关键字用于停止执行 JavaScript，并调用调试函数。
* 这个关键字与在调试工具中设置断点的效果是一样的。
* 如果没有调试可用，debugger 语句将无法工作。
* 开启 debugger ，代码在第三行前停止执行。
```js
var x = 15 * 5;
debugger;
document.getElementbyId("demo").innerHTML = x;
```
> 话说调试之类的我一直不是很会.....有时间要好好学学


<br/>

# 二十七. JS 变量提升

### (1) JS 变量提升
JavaScript 中，变量可以在使用后声明，也就是变量可以先使用再声明。

以下两个实例将获得相同的结果：
```js
x = 5; // 变量 x 设置为 5

elem = document.getElementById("demo"); // 查找元素 
elem.innerHTML = x;                     // 在元素中显示 x

var x; // 声明 x
```
```js
var x; // 声明 x
x = 5; // 变量 x 设置为 5

elem = document.getElementById("demo"); // 查找元素 
elem.innerHTML = x;                     // 在元素中显示 x
```

> **变量提升：函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部。**

### (2) JavaScript 初始化不会提升
JavaScript 只有声明的变量会提升，初始化的不会。


以下代码中 y 输出了 undefined，这是因为变量声明 (var y) 提升了，但是初始化(y = 7) 并不会提升，所以 y 变量是一个未定义的变量。
```js
var x = 5; // 初始化 x

elem = document.getElementById("demo"); // 查找元素 
elem.innerHTML = x + " " + y;           // 显示 x 和 y

var y = 7; // 初始化 y
```

<br/>

# 二十八. JS 严格模式(use strict)

### (1) 严格模式声明
严格模式通过在脚本或函数的头部添加 "use strict"; 表达式来声明
```js
<script>
"use strict";
x = 3.14;       // 报错 (x 未定义)
</script>
```
以上会报错:
```js
Uncaught ReferenceError: x is not defined
```
#### 另外: 
在函数内部声明是局部作用域 (只在函数内使用严格模式):
> 如果只在函数内部声明 严格模式 则只影响函数内部, 不影响函数外部.


```js
x = 3.14;       // 不报错 
myFunction();

function myFunction() {
   "use strict";
    y = 3.14;   // 报错 (y 未定义)
}
```

### (2) 严格模式的限制
> 限制有很多, 还是看文档吧.

[参考菜鸟教程](http://www.runoob.com/js/js-strict.html)

<br/>

# 二十九. JS 使用误区

### (1) switch 语句
switch 语句会使用恒等计算符(===)进行比较:

以下实例会执行 alert 弹窗：
```js
var x = 10;
switch(x) {
    case 10: alert("Hello");
}
```

以下实例由于类型不一致不会执行 alert 弹窗：
```js
var x = 10;
switch(x) {
    case "10": alert("Hello");
}
```

### (2) 加法与连接注意事项
* 加法是两个数字相加。
* 连接是两个字符串连接。
* JavaScript 的加法和连接都使用 + 运算符。
```js
var x = 10 + 5;          // x 的结果为 15
var x = 10 + "5";        // x 的结果为 "105"
```

### (3) 浮点型数据使用注意事项
* JavaScript 中的所有数据都是以 64 位浮点型数据(float) 来存储。
* 所有的编程语言，包括 JavaScript，对浮点型数据的精确度都很难确定：
```js
var x = 0.1;
var y = 0.2;
var z = x + y            // z 的结果为 0.3
if (z == 0.3)            // 返回 false
```
为解决以上问题，可以用整数的乘除法来解决：
```js
var z = (x * 10 + y * 10) / 10;       // z 的结果为 0.3
```

### (4) 字符串分行
在字符串中直接使用回车换行是会报错的：
```js
var x = "Hello
World!";
```
字符串断行需要使用反斜杠`(\)`，如下所示:
```js
var x = "Hello \
World!";
```

### (5) Return 语句
```js
function myFunction(a) {
    var
    power = 10;  
    return
    a * power;
}
```
由于var是一个不完整的语句, 所以js将尝试读取第二行的语句. 由于return 是完整的, 所以js 将自动关闭语句, 下面的 a* power 就没有读取.


### (6) 数组中使用名字来索引
* 许多程序语言都允许使用名字来作为数组的索引。(使用名字来作为索引的数组称为关联数组(或哈希))
* JavaScript 不支持使用名字来索引数组，只允许使用数字索引。

正确(使用数字作为索引):
```js
person[0] = "John"; 
```
错误(使用名字作为索引):
```js
person["firstName"] = "John";
```

### (7) Undefined 不是 Null
> 没太看懂


* 在 JavaScript 中, null 用于对象, undefined 用于变量，属性和方法。
* 对象只有被定义才有可能为 null，否则为 undefined。
* 如果我们想测试对象是否存在，在对象还没定义时将会抛出一个错误。

错误的使用方式：
```js
if (myObj !== null && typeof myObj !== "undefined")
``` 
正确的方式是我们需要先使用 typeof 来检测对象是否已定义：
```js
if (typeof myObj !== "undefined" && myObj !== null) 
```

### (8) 程序块作用域
在每个代码块中 JavaScript 不会创建一个新的作用域，一般各个代码块的作用域都是全局的。

以下代码的的变量 i 返回 10，而不是 undefined：
```js
for (var i = 0; i < 10; i++) {
    // some code
}
return i;
```
> 之前说的是js中, 函数里面是作用域是局部. 这里说的是 普通代码块.

<br/>

# 三十. JS 表单
> 好像比较重要, 要仔细看


### (1) JavaScript 表单验证

以下实例代码用于判断表单字段(fname)值是否存在，如果存在，则弹出信息，否则阻止表单提交：
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script>
function validateForm() {
    var x = document.forms["myForm"]["fname"].value;
    if (x == null || x == "") {
        alert("需要输入名字。");
        return false;
    }
}
</script>
</head>
<body>

<!--注意onSubmit的作用-->
<form name="myForm" action="demo_form.php"
onsubmit="return validateForm()" method="post"> 
名字: <input type="text" name="fname">
<input type="submit" value="提交">
</form>

</body>
</html>
```

> 百度而来: onSubmit事件的作用是: 点击submit时, 调用相关的函数对表单进行初步的判断处理.

### (2) JS 验证输入的数字
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<h1>JavaScript 验证输入</h1>

<p>请输入 1 到 10 之间的数字：</p>
<!--输入框, 有id-->
<input id="numb">  
<!--点击按钮时调用myFunction()函数-->
<button type="button" onclick="myFunction()">提交</button>
<!--普通段落,确定id,为之后修改文字做准备-->
<p id="demo"></p>

<script>
function myFunction() {
    var x, text;

    // 获取 输入框为 id="numb" 的值
    x = document.getElementById("numb").value;

    // 如果输入的值 x 不是数字或者小于 1 或者大于 10，则提示错误 Not a Number or less than one or greater than 10
    if (isNaN(x) || x < 1 || x > 10) {
        text = "输入错误";
    } else {
        text = "输入正确";
    }
    //将text的值放入 id为demo 的段落中 
    document.getElementById("demo").innerHTML = text;
}
</script>

</body>
</html>
```

### (3) HTML 表单自动验证
> 如果设置了required属性，则规定在提交表单之前必须填写输入字段。也就是说, 这个表单必须得填, 不能为空.


HTML 表单验证也可以通过浏览器来自动完成。

如果表单字段 (fname) 的值为空, required 属性会阻止表单提交：

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<form action="demo_form.php" method="post">
  <input type="text" name="fname" required="required">
  <input type="submit" value="提交">
</form>

<p>点击提交按钮，如果输入框是空的，浏览器会提示错误信息。</p>

</body>
</html>
```

### (4) 其他
#### 典型的数据验证有：

* 必需字段是否有输入?
* 用户是否输入了合法的数据?
* 在数字字段是否输入了文本?

#### 服务端与客户端验证
* 服务端数据验证是在数据提交到服务器上后再验证.
* 客户端数据验证 side validation是在数据发送到服务器前，在浏览器上完成验证.

#### HTML 约束验证
* 约束验证 HTML 输入属性 (有很多, 自己看文档)
* 约束验证 CSS 伪类选择器 (有很多, 自己看文档)

<br/>

# 三十一. JS 表单验证

### (1) 必填（或必选）项目
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
</head>
<head>
<script>
function validateForm(){
var x=document.forms["myForm"]["fname"].value;
if (x==null || x==""){
  alert("姓必须填写");
  return false;
  }
}
</script>
</head>
<body>
	
<form name="myForm" action="demo-form.php" onsubmit="return validateForm()" method="post">
姓: <input type="text" name="fname">
<input type="submit" value="提交">
</form>
	
</body>
</html>
```

### (2) E-mail 验证
* 下面的函数检查输入的数据是否符合电子邮件地址的基本语法。

* 意思就是说，输入的数据必须包含 @ 符号和点号(.)。同时，@ 不可以是邮件地址的首字符，并且 @ 之后需有至少一个点号：
```js
function validateForm(){
  var x=document.forms["myForm"]["email"].value;
  var atpos=x.indexOf("@");
  var dotpos=x.lastIndexOf(".");
  if (atpos<1 || dotpos<atpos+2 || dotpos+2>=x.length){
    alert("不是一个有效的 e-mail 地址");
    return false;
  }
}
```

<br/>

# 三十二. JS 验证API
> 百度: API: 应用程序编程接口(Application Programming Interface), 是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。

### (1) 约束验证 DOM 方法
#### checkValidity()
 如果 input 元素中的数据是合法的返回 true，否则返回 false。

#### setCustomValidity()
> 没太看懂这是什么意思, 不过看懂代码就行了


设置 input 元素的 validationMessage 属性，用于自定义错误提示信息的方法。

使用 setCustomValidity 设置了自定义提示后，validity.customError 就会变成true，则 checkValidity 总是会返回false。如果要重新判断需要取消自定义提示，方式如下：

setCustomValidity('') 
setCustomValidity(null) 
setCustomValidity(undefined)

```js
<input id="id1" type="number" min="100" max="300" required>
<button onclick="myFunction()">验证</button>
 
<p id="demo"></p>
 
<script>
function myFunction() {
    //获取id为id1的输入框的内容
    var inpObj = document.getElementById("id1");
    //checkValidity()函数检查是否合理,判断依据主要是输入框里面定义的条件
    if (inpObj.checkValidity() == false) {
        //如果不正确则弹出自定义提示
        document.getElementById("demo").innerHTML = inpObj.validationMessage;
    }
}
</script>
```

### (2) 约束验证 DOM 属性
> 没太看懂.....


* validity	布尔属性值，返回 input 输入值是否合法
* validationMessage	浏览器错误提示信息
* willValidate	指定 input 是否需要验证

### (3) Validity 属性
input 元素的 validity 属性包含一系列关于 validity 数据属性

> 具体的自己看文档, 有很多...


#### 如果输入的值大于100, 显示一个信息:
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
</head>
<body>

<p>输入数字并点击验证按钮:</p>

<input id="id1" type="number" max="100">
<button onclick="myFunction()">验证</button>

<p>如果输入的数字大于 100 ( input 的 max 属性), 会显示错误信息。</p>

<p id="demo"></p>

<script>
function myFunction() {
    var txt = "";
    //validity.rangeOverflow作用: 当输入值比最大限制大的时候, 确定提示信息
    //validity属性中的rangeOverflow数据属性
    if (document.getElementById("id1").validity.rangeOverflow) {
        txt = "输入的值太大了";
    } else {
        txt = "输入正确";
    }
    document.getElementById("demo").innerHTML = txt;
}
</script>

</body>
</html>
```

#### 如果输入的值小于 100，显示一个信息：
```html
<input id="id1" type="number" min="100" required>
<button onclick="myFunction()">OK</button>
 
<p id="demo"></p>
 
<script>
function myFunction() {
    var txt = "";
    var inpObj = document.getElementById("id1");
    //判断是不是数字
    if(!isNumeric(inpObj.value)) {
        txt = "你输入的不是数字";
        //输入值比最小限制小
    } else if (inpObj.validity.rangeUnderflow) {
        txt = "输入的值太小了";
    } else {
        txt = "输入正确";
    }
    document.getElementById("demo").innerHTML = txt;
}
 
// 判断输入是否为数字
function isNumeric(n) {
    return !isNaN(parseFloat(n)) && isFinite(n);
}
</script>
```

<br/>

# 三十三. JS 保留关键字
在 JavaScript 中，一些标识符是保留关键字，不能用作变量名或函数名。

> 比较多, 具体看文档

<br/>

# 三十四. JS this 关键字
> 文档说的很多. 其实在定义一个类时,this就是这个类的一个对象,并且在类里面. 可以直接调用这个类里面的所有属性

例如:
```js
var person = {
  firstName: "John",
  lastName : "Doe",
  id       : 5566,
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};
```
当调用 `person.fullName();` 这个函数的时候, 会返回`John Doe`.

### (1) 单独使用 this
单独使用 this，则它指向全局(Global)对象。

在浏览器中，window 就是该全局对象,值为[object Window]:
```js
<script>
var x = this;
document.getElementById("demo").innerHTML = x;
</script>
```
返回:
```js
[object Window]
```

严格模式下，如果单独使用，this 也是指向全局(Global)对象。
```js
"use strict";
var x = this;
```
### (2) 函数中使用 this（默认）
> 在函数中，函数的所属者默认绑定到 this 上。

在浏览器中，window 就是该全局对象为 [object Window]:
```js
function myFunction() {
  return this;
}
```

### (3) 函数中使用 this（严格模式）
严格模式下函数是没有绑定到 this 上，这时候 this 是 undefined。
```js
"use strict";
function myFunction() {
  return this;
}
```
返回: 
```js
undefined
```

### (4) 事件中的 this
在 HTML 事件句柄中，this 指向了接收事件的 HTML 元素：
```js
<button onclick="this.style.display='none'">
点我后我就消失了
</button>
```
> this 指向`<button>`标签里面的元素, 这里的效果就是使`<button>`标签不见(不展示)

### (5) 显式函数绑定
* 在 JavaScript 中函数也是对象，对象则有方法
* apply 和 call 就是函数对象的方法。这两个方法异常强大，他们允许切换函数执行的上下文环境(context), 即 this 绑定的对象。
```js
var person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
var person2 = {
  firstName:"John",
  lastName: "Doe",
}
person1.fullName.call(person2);  // 返回 "John Doe"
```
返回:
```js
"John Doe"
```

<br/>

# 三十五. let 和 const
* ES2015(ES6) 新增加了两个重要的 JavaScript 关键字: let 和 const。
* 在 ES6 之前，JavaScript 只有两种作用域： 全局变量 与 函数内的局部变量。

### (1)全局变量
函数外声明的变量作用域时全局
普通代码块里面的变量的作用域是全局变量

### (2)局部变量
函数内声明的变量作用域是局部变量

### (3)块级作用域(Block Scope)
使用 var 关键字声明的变量不具备块级作用域的特性，它在 {} 外依然能被访问到。
```js
{ 
    var x = 2; 
}
// 这里可以使用 x 变量
```
ES6 可以使用 let 关键字来实现块级作用域。

let 声明的变量只在 let 命令所在的代码块 {} 内有效，在 {} 之外不能访问。
```js
{ 
    let x = 2;
}
// 这里不能使用 x 变量
```

### (4) HTML 代码中使用全局变量
* 在 JavaScript 中, 全局作用域是针对 JavaScript 环境。
* 在 HTML 中, 全局作用域是针对 window 对象。

使用 var 关键字声明的全局作用域变量属于 window 对象:
```js
var carName = "Volvo";
// 可以使用 window.carName 访问变量
```
使用 let 关键字声明的全局作用域变量不属于 window 对象:
```js
let carName = "Volvo";
// 不能使用 window.carName 访问变量
```

#### 重置变量
* 在相同的作用域或块级作用域中，不能使用 let 关键字来重置 var 关键字声明的变量:
* 在相同的作用域或块级作用域中，不能使用 let 关键字来重置 let 关键字声明的变量:
* 在相同的作用域或块级作用域中，不能使用 var 关键字来重置 let 关键字声明的变量:
* let 关键字在不同作用域，或不同块级作用域中是可以重新声明赋值的:

### (5) 变量提升
JavaScript 中，var 关键字定义的变量可以在使用后声明，也就是变量可以先使用再声明（JavaScript 变量提升）。
```js
// 在这里可以使用 carName 变量
 
var carName;
```
let 关键字定义的变量则不可以在使用后声明，也就是变量需要先声明再使用。
```js
// 在这里不可以使用 carName 变量

let carName;
```

### (6) const 关键字
const 用于声明一个或多个常量，声明时必须进行初始化，且初始化后值不可再修改：
```js
const PI = 3.141592653589793;
PI = 3.14;      // 报错
PI = PI + 10;   // 报错
```

### (7) 并非真正的常量
const 的本质: const 定义的变量并非常量，并非不可变，它定义了一个常量引用一个值。使用 const 定义的对象或者数组，其实是可变的。下面的代码并不会报错：
#### 常量对象:
```js
// 创建常量对象
const car = {type:"Fiat", model:"500", color:"white"};
 
// 修改属性:
car.color = "red";
 
// 添加属性
car.owner = "Johnson";
```

但是我们不能对常量对象重新赋值：
```js
const car = {type:"Fiat", model:"500", color:"white"};
car = {type:"Volvo", model:"EX60", color:"red"};    // 错误
```

#### 常量数组：
```js
// 创建常量数组
const cars = ["Saab", "Volvo", "BMW"];
 
// 修改元素
cars[0] = "Toyota";
 
// 添加元素
cars.push("Audi");
```
但是我们不能对常量数组重新赋值：
```js
const cars = ["Saab", "Volvo", "BMW"];
cars = ["Toyota", "Volvo", "Audi"];    // 错误
```

### (8) const的变量提升
* JavaScript var 关键字定义的变量可以在使用后声明，也就是变量可以先使用再声明（JavaScript 变量提升）。
* const 关键字定义的变量则不可以在使用后声明，也就是变量需要先声明再使用。

<br/>

# 三十六. JS JSON
* JSON 是用于存储和传输数据的格式。
* JSON 通常用于服务端向网页传递数据 。
* JSON 是一种轻量级的数据交换格式。
* JSON是独立的语言 
* JSON 易于理解。
*  JSON 使用 JavaScript 语法，但是 JSON 格式仅仅是一个文本

### (1) JSON 实例
以下 JSON 语法定义了 sites 对象: 3 条网站信息（对象）的数组:
```js
{"sites":[
    {"name":"Runoob", "url":"www.runoob.com"}, 
    {"name":"Google", "url":"www.google.com"},
    {"name":"Taobao", "url":"www.taobao.com"}
]}
```

### (2) JSON 数据 - 一个名称对应一个值
JSON 数据格式为 键/值 对，就像 JavaScript 对象属性。

格式:`字段名称:值`
```js
"name":"Runoob"
```
### (3) JSON 对象
就像在 JavaScript 中, 对象可以保存多个 键/值 对：
```js
{"name":"Runoob", "url":"www.runoob.com"}
```
### (4) JSON 数组
就像在 JavaScript 中, 数组可以包含对象：
```js
"sites":[
    {"name":"Runoob", "url":"www.runoob.com"}, 
    {"name":"Google", "url":"www.google.com"},
    {"name":"Taobao", "url":"www.taobao.com"}
]
```
在以上实例中，对象 "sites" 是一个数组，包含了三个对象。

每个对象为站点的信息（网站名和网站地址）

### (5) JSON 字符串转换为 JavaScript 对象
首先，创建 JavaScript 字符串，字符串为 JSON 格式的数据：
```js
var text = '{ "sites" : [' +
'{ "name":"Runoob" , "url":"www.runoob.com" },' +
'{ "name":"Google" , "url":"www.google.com" },' +
'{ "name":"Taobao" , "url":"www.taobao.com" } ]}';
```
然后，使用 JavaScript 内置函数 JSON.parse() 将字符串转换为 JavaScript 对象:
```js
var obj = JSON.parse(text);
```
最后，在页面中使用新的 JavaScript 对象：
```js
var text = '{ "sites" : [' +
    '{ "name":"Runoob" , "url":"www.runoob.com" },' +
    '{ "name":"Google" , "url":"www.google.com" },' +
    '{ "name":"Taobao" , "url":"www.taobao.com" } ]}';
    
obj = JSON.parse(text);
document.getElementById("demo").innerHTML = obj.sites[1].name + " " + obj.sites[1].url;
```
返回:
```js
Google www.google.com
```

### (6) 相关函数
* `JSON.parse()`	用于将一个 JSON 字符串转换为 JavaScript 对象。
* `JSON.stringify()`   用于将 JavaScript 值转换为 JSON 字符串。

<br/>

# 三十七. JS void
 void 是 JavaScript 中非常重要的关键字，该操作符指定要计算一个表达式但是不返回值。

下面的代码创建了一个超级链接，当用户点击以后不会发生任何事。
```js
<a href="javascript:void(0)">单击此处什么也不会发生</a>
```

以下实例中，在用户点击链接后显示警告信息：
```js
<a href="javascript:void(alert('Warning!!!'))">点我!</a>
```

### (1) href="#"与href="javascript:void(0)"的区别
* `#` 包含了一个位置信息，默认的锚是`#top`也就是网页的上端。
* 而javascript:void(0), 仅仅表示一个死链接。
```js
<a href="javascript:void(0);">点我没有反应的!</a>
<a href="#pos">点我定位到指定位置!</a>
```

<br/> 

# 三十八. JS 代码规范
### (1) 变量名推荐使用驼峰法来命名(camelCase):
```js
firstName = "John";
lastName = "Doe";
```

### (2) 空格与运算符
通常运算符 ( = + - * / ) 前后需要添加空格:
```js
var x = y + z; 
```

### (3) 代码缩进
通常使用 4 个空格符号来缩进代码块

### (4) 语句规则
#### 简单语句的通用规则
* 一条语句通常以分号作为结束符

#### 复杂语句的通用规则:
* 将左花括号放在第一行的结尾。
* 左花括号前添加一空格。
* 将右花括号独立放在一行。
* 不要以分号结束一个复杂的声明。

### (5) 对象规则
#### 对象定义的规则:
* 将左花括号与类名放在同一行。
* 冒号与属性值间有个空格。
* 字符串使用双引号，数字不需要。
* 最后一个属性-值对后面不要添加逗号。
* 将右花括号独立放在一行，并以分号作为结束符号。

### (6) 命名规则
> 	对于命名而言 `-` 通常在 JavaScript 中被认为是减法，所以不允许使用。


一般很多代码语言的命名规则都是类似的，例如:
* 变量和函数为小驼峰法标识, 即除第一个单词之外，其他单词首字母大写（ lowerCamelCase）
* 全局变量为大写 (UPPERCASE )
* 常量 (如 PI) 为大写 (UPPERCASE )


### (7) HTML 载入外部 JavaScript 文件
使用简洁的格式载入 JavaScript 文件 ( type 属性不是必须的):
```js
<script src="myscript.js">
```

### (8) 使用小写文件名
* 大多 Web 服务器 (Apache, Unix) 对大小写敏感： london.jpg 不能通过 London.jpg 访问。
* 其他 Web 服务器 (Microsoft, IIS) 对大小写不敏感： london.jpg 可以通过 London.jpg 或 london.jpg 访问。
* 建议统一使用小写的文件名。
