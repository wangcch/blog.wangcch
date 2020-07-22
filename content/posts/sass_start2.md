---
title: sass 入门（二）
date: 2018-01-20
categories:
- CSS
- sass
tags:
- CSS
- sass
---

1. [不同样式风格嵌套方式](#不同样式风格嵌套方式)
2. [普通变量与默认变量](#普通变量与默认变量)
3. [局部变量与全局变量](#局部变量与全局变量)
4. [嵌套](#嵌套)

<!-- more -->


# 不同样式风格嵌套方式

1. 嵌套输出方式 nested
2. 展开输出方式 expanded  
3. 紧凑输出方式 compact 
4. 压缩输出方式 compressed


## 嵌套输出方式 nested

编译时，添加 *--style nested* 参数

```
sass --watch demo.scss:demo.css --style nested
```

```scss
nav {
    li {
        display: inline-block;
    }
    a {
        text-decoration: none;
    }
}
```
```css
nav li {
    display: inline-block;}
nav a {
    text-decoration: none;}

<!--注意大括号-->

```

## 展开输出方式 expanded 
```
sass --watch demo.scss:demo.css --style expanded
```
```css
<!--sass 同上-->

<!--css-->
nav li {
    display: inline-block;
}
nav a {
    text-decoration: none;
}
```

## 紧凑输出方式 compact 
```
sass --watch demo.scss:demo.css --style compact
```
```css
<!--sass 同上-->

<!--css-->
nav li { display: inline-block; }
nav a { text-decoration: none; }
```

## 压缩输出方式 compressed
```
sass --watch demo.scss:demo.css --style compressed
```
```css
<!--sass 同上-->

<!--css-->
nav li{display:inline-block;}nav a{text-decoration:none;}

```

# 普通变量与默认变量

## 普通变量
```scss
$width: 200px;
.demo {
    width: $width;
}
```
编译之后
```css
.demo {
    width: 200px;
}
```
## 默认变量
sass 的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可。

```scss
$width: 200px !default;
.demo {
    width: $width;
}
```
编译之后
```css
.demo {
    width: 200px;
}
```
```scss
$width: 300px;
$width: 200px !default;
.demo {
    width: $width;
}
```
编译之后
```css
.demo {
    width: 300px;
}
```
# 局部变量与全局变量

```
$width: 200px !default; //定义全局变量
.demo {
    $width: 300px; //定义局部变量
    .test {
        width: $width;
    }
}
```

> 创建变量只适用于感觉确有必要的情况下。不要为了某些骇客行为而声明新变量，这丝毫没有作用。

# 嵌套
1. 选择器嵌套
2. 属性嵌套
3. 伪类嵌套

## 选择器嵌套

例如对于a标签的应用
```css
.demo a {
    color: #000;
}

.box .demo a {
    color: #fff;
}
```
sass选择器嵌套
```scss
.demo {
    a {
        color: #000;
        .box & {
            color: #fff;
        }
    }
}
```

## 属性嵌套

属性嵌套，CSS 的一些属性前缀相同，只是后缀不同

```css
.demo {
    font-size: 16px;
    font-weight: bold;
}
```
sass属性嵌套
```scss
.box {
    font: {
        size: 12px;
        weight: bold;
    }
}
```

## 伪类嵌套

```css
.demo:before {
    content: "伪类";
}
```
sass属性嵌套
```scss
.demo {
    $:before {
        content: "伪类";
    }
}
```

