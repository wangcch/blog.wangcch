---
title: sass 入门（三）
date: 2018-01-31
categories:
- CSS
- sass
tags:
- CSS
- sass
---

1. [混合宏](#混合宏)
2. [扩展/继承](#扩展/继承)
3. [占位符](#占位符 %placeholder)

<!-- more -->

# 混合宏
当相同的类型变得越来越多，简单的变量已经达不到我们的要求，这时我们就需要**混合宏**来帮我们完成。

## 声明混合宏

**1. 不带参数混合宏**

```scss
@mixin border-radius {
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```
<code>@mixin</code> 用于声明混合宏的关键词。<code>border-radius</code>为混合宏的名称
**2. 带参数混合宏**

```scss
@mixin border-radius($radius: 5px) {
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```
**3. 复杂混合宏**

简单来说就是添加了**逻辑关系**
```scss
@mixin box-shadow($shadow...) {
  @if length($shadow) >= 1 {
    @include prefixer(box-shadow, $shadow);
  } @else{
    $shadow:0 0 4px rgba(0,0,0,.3);
    @include prefixer(box-shadow, $shadow);
  }
}
```
当$shadow的参数数量大于等于1时，使用参数调用，反之则使用默认值。
> <code>...</code> 下面“混合宏参数”会提到，传递单个参数的值过多时使用

## 调用混合宏
使用 <code>@include</code> 调用
```scss
@mixin border-radius {
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```
调用
```scss
.demo {
    @include border-radius;
}
```
编译
```css
.demo {
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```

## 混合宏参数
混合宏传参的多种情形

**1. 不带值参数**

```scss
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```
调用
```scss
.demo {
    @include border-radius(5px);
}
```
编译
```css
.demo {
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```
**2. 带值参数（含有默认值）**

```scss
@mixin border-radius($radius:5px) {
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```
调用
```scss
.demo1 {
    @include border-radius;     //直接调用， 不带参数
}

.demo2 {
    @include border-radius(3px);     //带参数
}
```
编译
```css
.demo1 {
    -webkit-border-radius: 5px;
    border-radius: 5px;
}

.demo2 {
    -webkit-border-radius: 3px;
    border-radius: 3px;
}
```
**3. 多个参数**

字面意思，就是可以传多个参数
```scss
@mixin box($width, $height) {
    width: $width;
    height: $height;
}
```
```scss
.demo {
    @include box(200px, 200px);
}
```
```css
.demo {
    width: 200px;
    height: 200px;
}
```
> 特别参数<code>...</code>，传递单个参数的值过多时使用

```scss
@mixin box-shadow($shadows...) {
    -webkit-box-shadow: $shadow;
    box-shadow: $shadows;
}
```
在实际调用中：
```scss
.box {
  @include box-shadow(0 0 1px rgba(#000,.5), 0 0 2px rgba(#000,.2));
}
```
编译出来的CSS:
```css
.box {
  -webkit-box-shadow: 0 0 1px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.2);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.2);
}
```

# 扩展/继承
继承字面意思，类似java 子类继承父类。只不过这个继承是并存。
```scss
.btn {
    border-radius: 3px;
    border: 1px solid #ccc;
    padding: 10px;
}

.btn-primary {
    background-color: green;
    color: #fff;
    @extend .btn;
}

.btn-warn {
    background-color: red;
    color: #fff;
    @extend .btn;
}
```
编译
```css
.btn, .btn-primary, .btn-warn {
    border-radius: 3px;
    border: 1px solid #ccc;
    padding: 10px;
}

.btn-primary {
    background-color: green;
    color: #fff;
}

.btn-warn {
    background-color: red;
    color: #fff;
}
```
# 占位符 %placeholder
> 取代以前 CSS 中的基类造成的代码冗余的情形，如果不被 @extend调用的话，不会产生任何代码。

```scss
%pt15 {
    padding-top: 15px;
}

.demo1 {
    @extend %pt15;
}

.demo2 {
    @extend %pt15;
}
```
编译
```css
.demo1, .demo2 {
    padding-top: 15px;
}
```
> 通过 @extend 调用的占位符，编译出来的代码会将相同的代码合并在一起。


||混合宏|继承|占位符|
|--|--|--|--|
|声明方式|@mixin|.class|%placeholder|
|调用方式|@include|@extend|@extend|
|使用环境|如果相同代码需要在不同的环境传递不同的值，可以通过混合宏来定义重复使用的代码块。|相同代码已存在且无参数，可以调用已存在基类。|与继承基本类似，唯一不同的是，相同代码没有在基类中存在，而是需要额外声明。不调用则不会生成。|
