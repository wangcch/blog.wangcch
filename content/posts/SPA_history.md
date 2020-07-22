---
title: HTML5 History模式配置 (Node.js)
date: 2018-04-24
categories:
- js
- node.js
tags:
- express
- node.js
- router
---

> vue-router 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。如果不想要很丑的 hash，我们可以用路由的 history 模式，这种模式充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。
<!--more-->

> [Vue-router HTML5 History 模式](https://router.vuejs.org/zh-cn/essentials/history-mode.html)

简单来说为什么使用history模式呢？因为“#”，路由默认的是hash模式。

## 路由匹配区别：
```
// hash模式
http://demo.com/#/login


// history模式
http://demo.com/login
```

使用histroy模式时，不仅要配置路由，还需要后台配置支持。不然无法直接访问路由地址<code>demo.com/login</code> 。（前提：你也需要处理了404 默认页面问题）

**为什么要说记录一下node.js下使用history呢？很明显我也踩到了坑**

## 基于 Node.js 的 Express

对于 Node.js/Express (原生Node.js，可参考官方文档)

1.安装 [connect-history-api-fallback](https://github.com/bripkens/connect-history-api-fallback) 中间件 

```shell
npm install -s connect-history-api-fallback
```
2.引用

```js
var express = require('express');
var http = require('http');
var path = require('path');
var history = require('connect-history-api-fallback');

var app = express();
app.set('port', 2001);

app.use(history());         // !! 放在static静态资源的上面

// express 托管静态文件 ./public 文件夹下
app.use(express.static(path.join(__dirname, 'public')));

http.createServer(app).listen(app.get('port'), function () {
    console.log('static server start on port:' + app.get('port'));
});
```

是的这样就可以了。

> 参考: [Express配置SPA-History模式](https://www.xiejiahe.com/detail/59b264ae35f4275c5c081d06) (解答了我的问题)
