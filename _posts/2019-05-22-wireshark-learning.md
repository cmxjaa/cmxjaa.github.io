---
layout: post
title: "wireshark-learning"
date: 2019-05-22
author: jjnoob
categories:
- 2019-05
tags:
- web-sec
---

* content
{:toc}

> 计算机网络课要用, web-sec也要用到.

> 本文可以算得上是转载, 因为参考的这篇博客对菜鸟的我比较友好.

[参考-远有青山](https://blog.csdn.net/holandstone/article/details/47026213)

wireshark版本: win64-3.0.0汉化本


# 一. 背景
* wireshark是非常流行的网络封包分析软件, 功能十分强大. 可以截取各种网络封包, 显示网络封包的详细信息. 使用wireshark的人必须了解网络协议, 否则就看不懂wireshark.
* 为了安全考虑, wireshark只能查看封包, 而不能修改封包的内容, 或者发送封包.
* wireshark能获取HTTP，也能获取HTTPS，但是不能解密HTTPS，所以wireshark看不懂HTTPS中的内容. 总结, 如果是处理HTTP,HTTPS 还是用Fiddler, 其他协议比如TCP,UDP 就用wireshark.

<br />

# 二. 软件界面
打开软件, 选择wlan(因为连的是wifi). 可以看到已经开始抓包了.

从上往下大体分为5栏:
1. 显示过滤器 (Display Filter)
2. 封包列表 (Packet List Pane)
3. 封包详细信息 (Packet Details Pane)
4. 16进制数据 (Dissector Pane)
5. 地址栏 (Miscellanous)


<br />

# 三. Wireshark 显示过滤

过滤器会帮助我们在大量的数据中迅速找到我们需要的信息。

过滤器有两种: 
1. 一种是显示过滤器，就是主界面上那个，用来在捕获的记录中找到所需要的记录
2. 一种是捕获过滤器，用来过滤捕获的封包，以免捕获太多的记录. `在Capture -> Capture Filters` 中设置

过滤可以保存, 不同版本不一样.

<br />

# 四. 过滤表达式的规则
## (1) 协议过滤

比如TCP，只显示TCP协议。

## (2) IP 过滤

`ip.src ==192.168.1.102` 显示源地址为`192.168.1.102`

`ip.dst==192.168.1.102` 目标地址为`192.168.1.102`

## (3) 端口过滤

`tcp.port ==80`  端口为80的

`tcp.srcport == 80`  只显示TCP协议的愿端口为80的

## (4) Http模式过滤

`http.request.method=="GET"` 只显示`HTTP GET`方法的

## (5) 逻辑运算符为 AND/ OR

## (6) 常用的过滤表达式

`http`: 只查看HTTP协议的记录
`ip.src ==192.168.1.102 or ip.dst==192.168.1.102`: 源地址或者目标地址是`192.168.1.102`

<br />

# 五. 封包列表
(Packet List Pane)

封包列表的面板中显示的一行分别对应:
**编号, 时间戳, 源地址, 目标地址, 协议, 长度, 以及封包信息**

<br />

# 六. 封包详细信息 
(Packet Details Pane)

最重要的面板, 用来查看协议中的每一个字段

各行信息分别为:

* `Frame`:   **物理层**的数据帧概况
* `Ethernet II`: **数据链路层**以太网帧头部信息
* `Internet Protocol Version 4`: **互联网层**IP包头部信息
* `Transmission Control Protocol`:  **传输层**T的数据段头部信息, 例如: TCP.
* `Hypertext Transfer Protocol`:  **应用层**的信息, 例如: HTTP协议.

<br />

# 七. TCP包的具体内容
点开`Transmission Control Protocol`


```
Transmission Control Protocol, Src Port: 80, Dst Port: 57300, Seq: 0, Ack: 1, Len: 0
    Source Port: 80
    Destination Port: 57300
    [Stream index: 23]
    [TCP Segment Len: 0]
    Sequence number: 0    (relative sequence number)
    [Next sequence number: 0    (relative sequence number)]
    Acknowledgment number: 1    (relative ack number)
    1000 .... = Header Length: 32 bytes (8)
  > Flags: 0x012 (SYN, ACK)
    Window size value: 29200
    [Calculated window size: 29200]
  > Checksum: 0x251e [unverified]
    [Checksum Status: Unverified]
    Urgent pointer: 0
  > Options: (12 bytes), Maximum segment size, No-Operation (NOP), No-Operation (NOP), SACK permitted, No-Operation (NOP), Window scale
  > [SEQ/ACK analysis]
  > [Timestamps]
```


可以看到里面捕获的TCP包中的每个字段与**`TCP`报文格式**相对应:
* `Source port`: 源端口号
* `Destination port`: 目的端口号
* `Sequence number`: 序号
* `Acknowledgment number`: 确认号
* `Header length`: 报头长度
* `Flags`: 标志位
* `Window size value`: 窗口
* `Checksum`: 校验和


<br />

# 八. 三次握手
打开wireshark, 浏览器随便访问一个网站.

wireshark设置http过滤, 随便选中一条http记录, 右击选中 追踪流 -> tcp流.


wireshark截获到了三次握手的三个数据包, 都是TCP. 第四个包才是HTTP的. 这说明HTTP的确是使用TCP建立连接的。

> 过程我还没看书, 没怎么看懂. 凌晨一点半了, 我该睡了.

