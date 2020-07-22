---
title: CSS 几种垂直居中分享
date: 2017-06-04
categories:
- CSS
tags:
- CSS
---

分享几种自己积累的垂直居中方法，感觉目前实现垂直居中的一种是绝对定位，物理位移来实现。另一种是通过特定布局属性来实现，如文中提到的flex弹性布局和table表格布局实现。
（努力后续持续更新...）
<!--more-->


## 绝对定位 （自适应）
DEMO01:
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Vertical center demo01</title>
<style type="text/css">
	div{
		width: 200px;
		height: 200px;
		background-color: #00f;
		position: absolute;
		margin: auto;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
	}
</style>
</head>
<body>
<div></div>
</body>
</html>
```
 
这种很容易理解，和水平居中（margin:auto）差不多，都是自适应。top和bottom自适应实现垂直居中，left和right自适应实现水平居中。重点是绝对定位，案例相对浏览器定位。

![demo1](http://120.77.32.127/ty_home//blogImg/2017060401.png)
先上一张图吧，后面和这效果差不多就不上了:(

## 绝对定位 （50%定位）
DEMO02:
基于demo01的基础上样式如下
```css
div{
	width: 200px;
	height:200px;
	background-color: #00f;
	position: absolute;
	top: 50%;
	margin-top: -100px;
	left: 50%;
	margin-left: -100px;
}
```

(50%定位)主要就是，绝对定位，demo02相对浏览器定位。<br>
div正方形上面距浏览器上边，浏览器高度的一半距离。<br>
div正方形左边距浏览器左边，浏览器宽度的一半的距离。<br>
此时可以知道div正方形的**左上顶点**位于浏览器的中心。所以之后的margin相对自己位移就很容易理解了，位移距离是div本身的一半。<br>
**缺点**：父元素空间不够时, 子元素可能不可见(当浏览器窗口缩小时,滚动条不出现时).如果子元素设置了overflow:auto, 则高度不够时, 会出现滚动条.

## 弹性布局 （flex）
DEMO03:
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>vertical center demo03</title>
<style type="text/css">
	html,body{
	height: 100%;
	display: flex;
	display: -webkit-flex;
	flex-direction: column; //	灵活的项目将垂直显示，正如一个列一样。
	-webkit-flex-direction: column;
	justify-content: center; // 垂直居中
	-webkit-justify-content: center;
	align-items: center; //水平居中
	-webkit-align-items: center;
}
div{
	width: 200px;
	height: 200px;
	background-color: #00f;
}
</style>
</head>
<body>
<div></div>
</body>
</html>
```
采用Flex布局的元素，称为Flex容器（flex container）。它的所有子元素自动成为容器成员，称为Flex项目（flex item）。而垂直实现也是通过容器的特定属性。<br>
flex布局详细讲解[flex布局](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

## 表格布局 （table）
DEMO04:
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>demo04</title>
<style type="text/css">
	*{margin:0;padding: 0;} //初始化。消除滚动条
	html,body{
		height: 100%;
	}
	.box{
		width: 100%;
		height: 100%;
		display: table;
	}
	.center{
		display: table-cell;
		vertical-align: middle;
		text-align: center;
	}
	.demo{
		width: 200px;
		height: 200px;
		background-color: rgb(0,0,0);
		margin:auto;
	}
</style>
</head>
<body>
	<div class="box">
		<div class="center">
			<div class="demo"></div>
		</div>
	</div>
</body>
</html>
```
display:table 使div:box元素作为块级元素显示，表格后带有换行符<br>
display:table-cell 使div:center元素作为一个表格单元格显示，此时div:center会填满div:box。<br>
vertical-align:middle实现父元素垂直中部显示。

努力继续更新。感谢：）
