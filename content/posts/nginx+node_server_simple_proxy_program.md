---
title: Nginx Node 服务器简单代理方案
date: 2018-03-25
categories:
- js
- node.js
tags:
- Nginx
- node.js
- pm2
---
简单使用Nginx反向代理Node服务

<!-- more -->

## 前言

一直处于todo状态的东西，但本人比较懒，一直没写，但却用了很久。应该是去年开始线上服务器从windows server转到CentOS。（windows server的傻瓜式操作确实很low）当然WS的应用太占内存（类似XAMPP的应用在我的1核1G的学生机根本不行，远程桌面都进不去，报内存不足），所以选择CentOS是必然结果。

好，回归正题：Nginx反向代理node服务，使用**pm2**做node服务管理。
> [pm2](http://pm2.keymetrics.io) 一个带有负载均衡功能的Node应用的进程管理器.

**为什么使用Nginx反向代理？**

很简单，nginx不会用。：）
好吧，当然Nginx 本身就是是一个很强大的高性能Web和反向代理服务器。

## 准备

1. install nginx
> [参考：CentOS yum install nginx](http://blog.theyear.space/2018/03/07/CentOS%20yum_install_nginx/#more)
2. install node
```shell
yum install node
```
3. install pm2
```shell
npm install pm2 -g
```

## node服务

1. 初始化
新建一个项目文件夹，创建一个 package.json 文件
```shell
mkdir demoapp
cd demoapp

npm init
```
2. express
> 使用 [express](http://www.expressjs.com.cn) 框架 (以使用express为例)
```shell
npm install express --save
```
3. 新建app.js
```shell
vim app.js
```
```js
// app.js

var express = require('express');
var http = require('http');
var path = require('path');

var app = express();
// 设置端口
app.set('port', 2000);
// express 托管静态文件 ./public 文件夹下
app.use(express.static(path.join(__dirname, 'public')));

http.createServer(app).listen(app.get('port'), function(){
  console.log('static server start on port:' + app.get('port'));
});
```
4. 创建静态文件目录
```shell
mkdir public
```
将你打包好的文件放置在public 文件夹下
5. 测试
```shell
node app.js
```
访问 you_ip:2000 查看是否可用，ctrl+c 关闭服务

## pm2进程管理

pm2 启动服务
```shell
pm2 start app.js
```

pm2 常用命令
```shell
# 显示PM2启动的所有的应用程序列表
pm2 list

# 停止app应用进程
pm2 stop APP_NAME
pm2 stop all # 停止所有，也可以指定id。 下同

# 重启应用
pm2 restart APP_NAME

# 删除应用
pm2 delete APP_NAME

# 显示每个应用程序的CPU和内存占用情况
pm2 monit

# 显示应用的所有信息
pm2 show APP_NAME
```

## nginx配置

上述配置完成，可以进行IP:PORT 进行访问，但还是无法使用域名，所以下面进行nginx反向代理配置。
进入nginx配置路径，并在conf.d添加自己的配置
```shell
cd /etc/nginx/conf.d
```
配置基本相同，在前缀加上node监听端口
```
# *.conf

upstream nodejs {
  server 127.0.0.1:2000; # 反向监听2000端口
  keepalive 64;
}
```
同一个域名域名下监听其他端口
```
# *.conf
# 例：you_domain/demo  监听服务器3000端口

location /demo/ {
    proxy_pass http://127.0.0.1:3000/;
}
```
