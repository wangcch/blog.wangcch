---
title: get put post delete 区别
date: 2017-11-10
categories:
- network
tags:
- network
---
|||
|------|------|
|GET | 查看|
|PUT | 更新与创建|
|POST | 创建|
|DELETE | 删除|

<!--more-->

## get
GET请求向数据库索取数据请求，从而获取信息。只是查询数据，不会修改和影响数据本身。

对于GET方式，浏览器会把http、header和data一并发送出去，服务器响应200。

## PUT
PUT请求是向服务器端发送数据，从而改变数据。类似于update, 用于改变数据的内容，并不会数据结构。

## post
POST请求与PUT类似，都是向服务器端发送数据。但会改变数据的类型与内容。

而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200。 （并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次）

## delete
DELETE请求是删除操作


参考：
[get、put、post、delete含义与区别](https://www.15yan.com/story/7dz6oXiSHeq/)