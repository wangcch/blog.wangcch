---
title: sass 入门（一）
date: 2018-01-18
categories:
- CSS
- sass
tags:
- CSS
- sass
---


## 简介
    
> Sass 是一门高于 CSS的元语言，它能用来清晰地、结构化地描述文件样式，有着比普通 CSS 更加强大的功能。Sass能够提供更简洁、更优雅的语法，同时提供多种功能来创建可维护和管理的样式表。
[来自官网sass-lang.com](http://sass-lang.com)

<!--more-->


## sass 与 scss

好吧，我开始也以为sass与scss是两个东西。其实是一种东西。但还是有一定的区别：
1.文件扩展名不同，Sass 是以“.sass”后缀为扩展名，而 SCSS 是以“.scss”后缀为扩展名。（以上废话）
2.语法书写方式不同，Sass 是以严格的缩进式语法规则来书写，不带大括号({})和分号(;)，而 SCSS 的语法书写和我们的 CSS 语法书写方式非常类似。
```
// sass
$color: #000;
.demo
    color: $color;

// scss
$color: #000;
.demo {
    color: $color;
}

```

## 安装

- mac
1. 检测Ruby 

```
// 查看ruby版本
ruby -v
// 没有ruby则安装
brew install ruby
```
2. 安装sass  （[离线下载](https://rubygems.org/gems/sass)）

```
// 在线安装
sudo gem install sass
// 离线安装 
sudo gem install 下载文件路径
// 查看sass版本
sass -v
```
- windows 

1. 下载安装Ruby

[http://rubyinstaller.org/downloads](http://rubyinstaller.org/downloads)

2. 安装sass (类似mac安装)

```
gem install sass
```
