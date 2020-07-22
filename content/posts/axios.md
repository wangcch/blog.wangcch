---
title: axios 好东西 
date: 2018-03-10
categories:
- js
- node.js
tags:
- js
- node.js
---
一个用于浏览器和node.js的基于Promise的HTTP客户端。
<!--more-->
为什么舍弃vue-resources? 因为vue-resources不再更新了， Vue2.0之后官方更推荐axios。而且axios也更强大。

> [github/axios](https://github.com/axios/axios)
浏览器支持
![axios](https://camo.githubusercontent.com/626c46cfd86214001b4143cda5d0ef27a25bd69f/68747470733a2f2f73617563656c6162732e636f6d2f6f70656e5f73617563652f6275696c645f6d61747269782f6178696f732e737667)

## 特征
1. 在浏览器中发送 XMLHttpRequests 请求
2. 在 node.js 中发送 http请求
3. 支持 Promise API
4. 拦截请求和响应
5. 转换请求和响应数据
6. 取消请求
7. 自动转换 JSON 数据
8. 客户端支持保护安全免受 CSRF/XSRF 攻击

## 安装
```
npm install axios
```
## 使用
```js
import axios from 'axios';
```
## get

```js
axios.get(url)
    .then(res => {
        console.log(res);
    }).catch(error => {
        console.log(error);
    });
```
> error.response 你会用到的

```js
axios.get(url)
   .catch(error => {
     if（error.response）{
        // 2XX 状态码之外的处理
        console.log（error.response.data）;
        console.log（error.response.status）;
        console.log（error.response.headers）;
     } else {
        // 在设置触发错误的请求时发生了错误
        console.log（'Error'，error.message）;
     }
   });
```
添加头部信息
```js
axios.get(url, {
        headers:{
            'Content-Type': 'multipart/form-data'
        }
    })
    .then(res => {
        console.log(res);
    }).catch(error => {
        console.log(error);
    });
```
## post

```js
axios.post(url, data)
    .then(res => {
        console.log(res);
    }).catch(error => {
        console.log(error);
    });
```
## more

```
axios.request(config)
axios.get(url[, config])
axios.delete(url[, config])
axios.head(url[, config])
axios.options(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
```
## 文档

github文档: [https://github.com/axios/axios](https://github.com/axios/axios)

看云中文文档：[https://www.kancloud.cn/yunye/axios/234845](https://www.kancloud.cn/yunye/axios/234845)

