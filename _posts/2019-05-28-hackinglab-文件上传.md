---
layout: post
title: "hackinglab-文件上传"
date: 2019-05-28
author: jjnoob
categories:
- 2019-05
tags:
- 文件上传
- web-sec
---

* content
{:toc}


> 因为这里的题目简单, 我又来了. 对, 我就是那个只会做简单题目的菜鸟.



# 一. 请上传一张jpg格式的图片
前端验证. 查看源码, 在html里看到:
```html
<script>
	function check(){
		var filename=document.getElementById("file");
		var str=filename.value.split(".");
		var ext=str[str.length-1];
		if(ext=='jpg'){
			return true;
		}else{
			alert("请上传一张JPG格式的图片！")
			return false;
		}
		return false;
	}
</script>
```


选择本地一个`t.php`文件改后缀为`t.jpg`. 上传. 刷新页面, burp抓包, 修改request里面的`t.jpg`为`t.php`, forward即可.

<br />

# 二. 请上传一张jpg格式的图片
做法和第一题一样.


<br />


# 三. 请上传一张jpg格式的图片
html源码中的js:
```js
<script>
	function check(){
		var filename=document.getElementById("file");
		var str=filename.value.split(".");
		var ext=str[1];
		if(ext==='jpg'){
			return true;
		}else{
			alert("请上传一张JPG格式的图片！");
			return false;
		}
		return false;
	}
</script>
```
三道题的js源码的作用都是用`.`分割文件名, 并验证其中的一部分. 看Js源码不难发现, 第一题是验证最后一个小数点的后面部分, 第三道题是验证第一个小数点的后面部分.


做法大体同上, 只是构造:`xxx.jpg.cpp`
