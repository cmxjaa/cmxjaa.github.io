---
layout: post
title: "Go-Studying"
date: 2019-04-18
author: duckduckk
category: 2019-04
tags: web
finished: true
---

> golang......wenku.....

> 这次的学习笔记博文写的很简洁, 很喜欢这种简洁.

[参考](http://www.runoob.com/go/go-tutorial.html)

1. `:=`是声明符号, 左边必须是一个新声明的变量
2. 声明变量: `var b string = "abc"`, 顺序有所不同, 变量类型在变量后面.
3. iota 特殊常量, 在const 关键字出现时将被重置为 0. const 中每新增一行常量声明将使 iota 计数一次.
4. `$`返回变量存储地址, `*` 指针变量
5. select 语句: select 是go 中一个控制结构, 类似于用于通信的 switch 语句, 每个 case 必须是一个通信操作, 要么是发送要么是接受, select 随机执行一个可运行的 case, 如果没有 case 可运行, 他将阻塞, 所以应当有一个默认的子句是可运行的.
6. 无限循环语句
  ```go
  for true{
      ...
  } 
  ```
7. golang 中, 左花括弧不可单独为一行, 右花括弧可以单独为一行.
8. for 循环的 range 格式:
    ```go
    for key, value := range oldMap{
        newMap[key]=value
    }
    ```
9. 函数:
    ```go
    func max(num1, num2 int) int {
        ...
        return result
    }
    ```
    * go 语言可返回多个值
    * 传递类型 有 值传递 和 引用传递
    * 引用传递函数声明: 
      ```go
      func swap (x *int , y * int ){

      }
      ```
    * 引用传递函数调用: `swap(&a, &b)`
10. go 语言的匿名函数可作为闭包
> 数据结构.....

11. 数组: 声明:
    ```go
    var balance =[5]float32 {
        1000.0, 2.0, 3.4, 7.0, 50.0
    }
    ```
    不设数组大小, 则 
    ```go
    var balance =[...]float32 {
        ...
    }
    ```
12. 指向指针的指针. 一个指针变量存放的 又是另一个指针变量的地址, `var ptr ** int` (指向指针的 指针变量为整型)
13. go 空指针的值为 `nil`
14. Go 语言结构体
    ```go
    type Books struct {
        title string
        author string
        subject string
        book_id int
    }
    func main() {
        // 创建一个新的结构体
        fmt.Println(Books{"Go 语言", "www.runoob.com", "Go 语言教程", 6495407})
    
    }
    ```
    * 访问结构体成员, 使用点号 `.` 操作符: `Book1.title = "Go 语言"`
> 越来越觉得, 这个golang的教程像CPP..指针什么的, 指针的指针什么的.

15. 切片(Slice)
    golang 数组的长度不可改变, 而切片(动态数组)的长度是不固定的.
    ```go
    func main() {
        //声明一个切片, int为类型, 3为初始长度, 5为最大长度
        var numbers = make([]int,3,5)
        printSlice(numbers)
    }

    func printSlice(x []int){
        //len()返回切片长度, cap()返回切片最长可达到的长度
        fmt.Printf("len=%d cap=%d slice=%v\n",len(x),cap(x),x)
    }
    ```
    * 输出:
    ```go
    len=3 cap=5 slice=[0 0 0]
    ```
    * 输出切片:
    ```go
    printSlice(numbers)
    ```
    * 向切片中添加元素:
    ```go 
    numbers = append(numbers, 2,3,4)
    printSlice(numbers)
    ```
    * 拷贝 numbers 的内容到 numbers1
    ```go
    copy(numbers1,numbers)
    ```
16. golang 空白符`_`


17. Map(集合)
    * key-value 对
    * 实例: 
      ```go
      //两种创建集合的方式
      var countryCapitalMap map[string]string /*创建集合 */
      countryCapitalMap = make(map[string]string)

      /* map插入key - value对,各个国家对应的首都 */
      countryCapitalMap [ "France" ] = "Paris"
      countryCapitalMap [ "Italy" ] = "罗马"
      countryCapitalMap [ "Japan" ] = "东京"
      countryCapitalMap [ "India " ] = "新德里"

      /*使用键输出地图值 */ 
      for country := range countryCapitalMap {
          fmt.Println(country, "首都是", countryCapitalMap [country])
      }
      ```    
    * delete() 函数用于删除集合的元素

    > 菜鸟教程 golang 竟然还讲递归... cpp

18. 语言类型转换
    整型转换成浮点型
    ```go
    float32(sum)
    ```
19. 语言接口
    ```go
    package main

    import (
        "fmt"
    )

    type Phone interface {
        call()
    }

    type NokiaPhone struct {
    }

    func (nokiaPhone NokiaPhone) call() {
        fmt.Println("I am Nokia, I can call you!")
    }

    type IPhone struct {
    }

    func (iPhone IPhone) call() {
        fmt.Println("I am iPhone, I can call you!")
    }

    func main() {
        var phone Phone

    phone = new(NokiaPhone)
    phone.call()

    phone = new(IPhone)
    phone.call()

    }
    ```
    输出:
    ```
    I am Nokia, I can call you!
    I am iPhone, I can call you!
    ```
    * 我们定义了一个接口Phone，接口里面有一个方法call()。
    * Go 语言提供了另外一种数据类型即接口，它把所有的具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口。
20. 错误处理
    > 没看, 因为觉得目前用不到, 以后如果有需要再看.
21. go 并发
    ```go
    func main() {
        //say()为前面代码定义的函数. 两个say()函数会同时进行--并发
        go say("world")
        say("hello")
    }
    ```
    * 通道（channel）
        ```go
        ch <- v    // 把 v 发送到通道 ch
        v := <-ch  // 从 ch 接收数据
            // 并把值赋给 v
        ```
        声明通道:
        ```go
        ch := make(chan int)
        ```
        > 个人理解: 所谓通道就是 先把多个数据放进通道里, 再在输出时输出, 有点类似于栈


    * 通道缓冲区
    通道可以设置缓冲区，通过 make 的第二个参数指定缓冲区大小：
        ```go
        ch := make(chan int, 100)
        ```
    * Go 遍历通道与关闭通道
        关闭:
        ```go
        close(c)
        ```
        Go 通过 range 关键字来实现遍历读取到的数据:
        ```go
        for i := range c {
            fmt.Println(i)
        }
        ```

