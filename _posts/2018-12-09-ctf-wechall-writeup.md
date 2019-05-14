---
layout: post
title: "ctf-wechall-writeup"
date: 2018-12-09
author: jjnoob
categories:
- 2018-12
tags:
- ctf
---

> ### 小渣渣来水 wechall

# **Training: Get Sourced (Training)**

摁下 Fn+f12 就可以看到网页源代码，done.

# **Training: Stegano I (Training, Stegano)**

1,下载该图片，用16进制编辑器(例如hex editor)打开该图片就可以找到flag，done.

2,也可以用vim打开该图片.
```
:%!xxd             // 将当前文本转换为16进制格式。
:%!xxd -r          // 将当前文件转换回文本格式。
```

# **Training: Crypto - Caesar I (Crypto, Training)**

凯撒密码问题，我使用cpp代码解决的

```c++
#include<stdio.h>
#include<string.h>
int main()
{
	int len;
	char an[100]={0};
	fgets(an,100,stdin);
	len=strlen(an);
	for(int i=1;i<26;i++)
	{
		for(int j=0;j<len;j++)
		{
			if(an[j]>='A'&&an[j]<='Z')
			{
				if(an[j]+i>'Z')
					printf("%c",an[j]+i-26);
				else
					printf("%c",an[j]+i);
			}
			else
				printf("%c",an[j]);
		}
		putchar('\n');
		putchar('\n');
	}
	return 0;
 } 
```

# **Training: WWW-Robots (HTTP, Training)**

先访问 http://www.wechall.net/robots.txt
得到
```
User-agent: *
Disallow: /challenge/training/www/robots/T0PS3CR3T


User-agent: Yandex
Disallow: *
```
再访问 http://www.wechall.net/challenge/training/www/robots/T0PS3CR3T

# **Training: ASCII (Training, Encoding)**

我使用py代码解决的
```python
a=input('Please enter:')
a = a.split(', ')
for each in a:
    print(chr(int(each)),end = '')
```

# **Encodings: URL (Training, Encoding)**

url解码问题

url解码的py3代码：
```python
from urllib.parse import unquote,quote
url2 =input('Please enter:')
url = unquote(url2)
print(url)
```
另外，url编码的py3代码：
```python
from urllib.parse import unquote,quote
url1 =input('Please enter Chinese:')
url = quote(url1)
print(url)
```

# **Prime Factory (Training, Math)**

我使用cpp代码解决的，用了long long 型，话说其实用string 型其实更好，但是为了能够在必要的时候拼凑常用的函数代码，形成临时cpp代码的方便，就没用了。
```c++
#include<iostream>
using namespace std;

int IsPrime(long long  m)//求素数函数
{
  int i;
  for(i=2;i<m;i++)
    {
      if(m%i==0)
	return 0;//不是素数
    }
  return 1;//是素数
}

long long fsum(long long  num)//求各个位数的数字之和
{
   long long sum = 0;
    while(num)
     {
         sum += num % 10;
         num /= 10;
     }
    return sum;
 
}
int main()
{
 
  int cnt=0;
  for(long long  i=1000000+1;cnt<2;i++)
    {
      if(IsPrime(i)&&IsPrime(fsum(i)))
	{
	  cout<<i<<endl;
	  cnt++;}
      
    }
  return 0;
}
```

> ## 未完待续，先睡会。。。。

> ## 续，12月18日

# **Training: Encodings I (Training, Encoding)**

* 首先需要一个配置好的oracle jdk环境
* 下载提供的JPK，运行
* 将01编码粘贴到Bianry->Bianry To Ascii中，通过Bianry->Bianry Format化为8位一组；
* Bianry->Bianry To Ascii，将编码转为ASCII码，发现为乱码，查原因发现8位一组时，多了一位0；
* 尝试将01编码化为7个一组，将BitsperBlock更改为7，发现刚好分完；
* Bianry->Bianry To Ascii，出现了正确的ASCII字符串：This text is 7-bit encoded ascii. Your password is easystarter.

# **Training: Programming 1 (Training, Coding)**

> ### 和cookies有关，看了网上的python代码，运行了，但是没有结果。。。。这题待定吧。

# **Training: Regex (Training, Regex)**

* 正则表达式

Answer:
```
level 1:
/^$/
level 2:
/^wechall$/
level 3:
/^wechall4?\.(?:jpg|gif|tiff|bmp|png)$/
level 4:
/^(wechall4?)\.(?:jpg|gif|tiff|bmp|png)$/
```


# **Training: PHP LFI (Exploit, PHP, Training)**

* 考虑%00截断
* 根据提示 要访问一个../solution.php

在URL后添加：
```php
?file=../solution.php%00
```
显示没有这个文件
再往上一级访问：
```php
?file=../../solution.php%00
```
done.

# **PHP 0817 (PHP, Exploit)**

* 这段php代码会根据_GET数组中which的值进行选择执行

在URL后添加
```php
?which=solution
```
done.

# **Training: Crypto - Transposition I (Crypto, Training)**

> ### 本题待定。。。。

我真的很菜很菜，要努力哦

> ## END

