---
title: CSS 清除float浮动
date: 2017-06-12
categories:
- CSS
tags:
- CSS
---

使用浮动的情况有很多，比如页面布局(`float:left` `float:right`)、取消块元素的独占一行等等。浮动对页面的主要影响是，当父盒子没有设置高，子盒子在父盒子中进行浮动。由于父盒子的高度为0，下面的元素会自动补位。这时候需要清除浮动影响。还有一点是今天遇到的所以准备整理一下，就是有些响应式界面并不是清除浮动，而是对浮动的去除。

<!--more-->

## float属性

float 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，使文本围绕在图像周围，不过在 CSS 中，任何元素都可以浮动。浮动元素会生成一个块级框，而不论它本身是何种元素。
如果浮动非替换元素，则要指定一个明确的宽度；否则，它们会尽可能地窄。
注释：假如在一行之上只有极少的空间可供浮动元素，那么这个元素会跳至下一行，这个过程会持续到某一行拥有足够的空间为止。

值 | 描述
-------|-------
left | 元素向左浮动
right | 元素向右浮动
none | 默认值。元素不浮动
inherit | 规定应该从父元素继承 float 属性的值。

今天就是没想到none,纠结了半天（	`clear:both`）。后来查了[w3]('http://www.w3school.com.cn/cssref/pr_class_float.asp')，瞬间就知道是自己理解错了。响应式样式浮动去除可以直接用`float:none`。

接下来我们就来了解了解浮动`float`
## 浮动产生的副作用

简单归纳就是
1.父级元素不能被撑开。会导致父元素背景颜色图片无法正常显示，父级元素边框也不能随内容而变化。
2.也会导致父级元素之间设置的`padding` `margin`属性不能正确表达，特别是上下边。

## 清除浮动

1.加额外标签（`clear:both`）

```html
<div>
	<div style="float:left;"></div>
	<div style="float:right;"></div>
	<div style="clear:both;"></div>//设置一个空标签
</div>
```

在浮动的盒子之下再放一个标签，在这个标签中使用clear:both，来清除浮动对页面的影响。
内部标签：将会浮动盒子的父盒子高度重新撑开。
外部标签：将会清除浮动盒子的影响，但不会撑开父盒子

2.overflow

```html
<div style="overflow:hidden;">
	<div style="float:left；"></div>
	<div style="float:right；"></div>
</div>
```

清除这个父元素的子元素浮动对页面的影响。**注意：**但`overflow:hidden`将会把超出的部分隐藏起来

3.伪元素（after）


```css
.clear:after{
	content:"";
	height:0;
	line-height:0;
	display:block; //块级元素
	visibility:hidden; //将元素隐藏
	clear:both;
}
.clear{
	zoom:1; //兼容IE
}
```

```html
<div class="clear">
	<div style="float:left；"></div>
	<div style="float:right；"></div>
</div>

```


原理和第一种差不多，不过是添加伪元素。`zoom`兼容ie6、7。相比优点浏览器的支持较好，不会出现怪问题。


一般推荐使用方法三，伪元素。感谢：）


