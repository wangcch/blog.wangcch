---
title: sass 入门（四）
date: 2018-02-04
categories:
- CSS
- sass
tags:
- CSS
- sass
---

1. [插值#{}](#插值#{})
2. [运算](#运算)
3. [控制指令](#控制指令)

<!-- more -->

# 插值#{}

```scss
@mixin set-value($side, $value) {
    margin-#{$side}: $value;
}

.demo {
    @include set-value(top, 15px);
}
```
编译
```css
.demo {
    margin-top: 15px;
}
```
用处无限大，等待你发掘。


# 运算
## 加法
```scss
$box-width: 100px;
$item-width: 50px;
.demo {
    width: $box-width - $item-width;
}
```
```css
.demo {
    width: 50px;
}
```
> 不同的单位类型相加会报错

## 减法
<code>-</code>  同理
## 乘法
<code>*</code>  同理
## 除法
<code>/</code>  同理

# 控制指令
## @if
根据条件除处理样式块
```scss
@mixin none ($boolean: true) {
    @if $boolean {
        display: block;
    }
    @else {
        display: none;
    }
}

.demo {
    @include none(false);
}
```
编译
```css 
.demo {
    display: none;
}
```
## @for 循环
```
@for $i from <start> through <end>   // 循环包含end数
@for $i from <start> to <end>       // 循环不包括end数
```
- <code>$i</code> 变量
- <code>start</code> 起始值
- <code>end</code> 结束值

**1. through**

```scss
@for $i from 1 through 3 {
    .demo#{$i} {
        margin-top: 10px * $i;
    }
}
```
编译
```css
.demo1 {
    margin-top: 10px;
}

.demo2 {
    margin-top: 20px;
}

.demo3 {
    margin-top: 30px;
}
```
**2. to**

```scss
@for $i from 1 to 3 {
    .demo#{$i} {
        margin-top: 10px * $i;
    }
}
```
编译
```css
.demo1 {
    margin-top: 10px;
}

.demo2 {
    margin-top: 20px;
}
```
## while 循环
只要...就...
```scss
$tot = 3;

@while $tot > 0 {
    .demo#{$tot} {
        margin-top: 10px * $tot;
    }
    $tot: $tot - 1;
}
```
编译
```css
.demo3 {
    margin-top: 30px;
}

.demo2 {
    margin-top: 20px;
}

.demo1 {
    margin-top: 10px;
}
```
## each 循环
遍历一个列表
```
@each $var in <list>
```

```scss
$list: one two three;

@mixin imgs {
    @each $img in $imgs {
        .img-#{$img} {
            background: url("/imgs/#{$img}.png");
        }
    }
}

.show-img {
    @include imgs;
}
```
编译
```css
.show-img .img-one {
    background: url("/imgs/one.png");
}

.show-img .img-two {
    background: url("/imgs/two.png");
}

.show-img .img-three {
    background: url("/imgs/three.png");
}
```