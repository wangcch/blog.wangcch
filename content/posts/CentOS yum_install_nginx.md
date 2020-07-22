---
title: CentOS yum install nginx
date: 2018-03-07
categories:
- Nginx
tags:
- CentOS
- Nginx
---

> CentOS 7

```
yum install -y nginx
```
<!-- more -->

## 安装Nginx源

```
rpm -ivh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```
/etc/yum.repos.d/ -> nginx.repo

## 安装Nginx

```
yum install -y nginx
```
```
# 输入命令
whereis nginx

# 输出
nginx: /usr/sbin/nginx /usr/lib64/nginx /etc/nginx /usr/share/nginx

#
# /etc/nginx  Nginx 配置路径
#
```
## 常用命令

```
# 启动
nginx

# 测试配置
nginx -t

# 重启
nginx -s reload

# 关闭
nginx -s stop
# 优雅关闭(不接受新的连接请求，等待旧的连接请求处理完毕再关闭)
nginx -s quit

# nginx版本信息
nginx -v

# nginx版本信息，编译版本，和配置参数
nginx -V
```

