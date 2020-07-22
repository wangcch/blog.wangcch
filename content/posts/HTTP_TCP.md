---
title: HTTP与TCP的区别
date: 2017-06-07
categories:
- network
tags:
- network
- HTTP
---
TCP是传输层，http是应用层。http是要基于TCP连接基础上的，TCP就是单纯建立连接，不涉及任何我们需要请求的实际数据，简单的传输。http是用来收发数据，即实际应用。
<!--more-->


# TCP/IP协议
Transmission Control Protocol/Internet Protocol，中译名为传输控制协议/因特网互联协议，又名网络通讯协议，是Internet最基本的协议、Internet国际互联网络的基础，由网络层的IP协议和传输层的TCP协议组成。

## TCP
TCP是面向连接的通信协议，通过三次握手建立连接，通讯完成时要拆除连接，由于TCP是面向连接的所以只能用于端到端的通讯。

当然**三次握手**也是相当经典：

第一次握手：建立连接时，客户端发送syn包（syn=j）到服务器，并进入SYN_SENT状态，等待服务器确认；SYN：同步序列编号（Synchronize Sequence Numbers）。

第二次握手：服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；

第三次握手：客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK(ack=k+1），此包发送完毕，客户端和服务器进入ESTABLISHED（TCP连接成功）状态，完成三次握手

对于一个已经建立的连接，TCP使用改进的三次握手来释放连接。**TCP关闭连接**的步骤：

第一步，当主机A的应用程序通知TCP数据已经发送完毕时，TCP向主机B发送一个带有FIN附加标记的报文段（FIN表示英文finish）。

第二步，主机B收到这个FIN报文段之后，并不立即用FIN报文段回复主机A，而是先向主机A发送一个确认序号ACK，同时通知自己相应的应用程序：对方要求关闭连接（先发送ACK的目的是为了防止在这段时间内，对方重传FIN报文段）。

第三步，主机B的应用程序告诉TCP：我要彻底的关闭连接，TCP向主机A送一个FIN报文段。

第四步，主机A收到这个FIN报文段后，向主机B发送一个ACK表示连接彻底释放。


## IP
网络之间互连的协议（Internet Protocol),包括A,B,C,D,E五个协议。
1. IP定义了在TCP/IP互联网上数据传送的基本单元和数据格式。
2. IP软件完成路由选择功能，选择数据传送的路径。
3. IP包含了一组不可靠分组传送的规则，指明了分组处理、差错信息发生以及分组的规则。

# HTTP协议
超文本传输协议（HTTP，HyperText Transfer Protocol)是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准。是Web联网的基础，也是手机联网常用的协议之一，HTTP协议是建立在TCP协议之上的一种应用。
HTTP连接最显著的特点是客户端发送的每次请求都需要服务器回送响应，在请求结束后，会主动释放连接。从建立连接到关闭连接的过程称为“一次连接”。

1.在HTTP 1.0中，客户端的每次请求都要求建立一次单独的连接，在处理完本次请求后，就自动释放连接。

2.在HTTP 1.1中则可以在一次连接中处理多个请求，并且多个请求可以重叠进行，不需要等待一个请求结束后再发送下一个请求。

# HTTP与TCP的区别

1. TCP是传输层，http是应用层
2. TCP是底层通讯协议，定义的是数据传输和连接方式的规范
3. HTTP是应用层协议，定义的是传输数据的内容的规范
4. HTTP协议中的数据是利用TCP协议传输的，所以支持HTTP也就一定支持TC
5. HTTP支持的是www服务。而TCP/IP是协议，它是Internet国际互联网络的基础。TCP/IP是网络中使用的基本的通信协议。 
6. TCP/IP实际上是一组协议，它包括上百个各种功能的协议，如：远程登录、文件传输和电子邮件等，而TCP协议和IP协议是保证数据完整传输的两个基本的重要协议。通常说TCP/IP是Internet协议族，而不单单是TCP和IP。


**参考**

[HTTP协议]('http://baike.baidu.com/link?url=ONOTU4pWTKuIBWSAdazMBwD-rIaqwUEbZuigqwOjHPwdOOLOrg9yQVH8qEw2X_S4Y-ND8KuyNQUHy6p-cSgaYPz8ENwMCcTxxOvYRlFbvxiO7l5NltC9bMcSMu_gAB8b7nuwWArLa-z7OPhO_zL4ia')
[三次握手]('http://baike.baidu.com/item/%E4%B8%89%E6%AC%A1%E6%8F%A1%E6%89%8B')
[TCP/IP协议]('http://baike.baidu.com/item/TCP%2FIP%E5%8D%8F%E8%AE%AE')