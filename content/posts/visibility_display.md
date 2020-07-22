---
title: CSS visibility与display可见性区别
date: 2017-06-02
categories:
- CSS
tags:
- CSS
- visibility
- display
---

主要区别：<br>

	visibility:hidden//设置的不可见的元素任然会占据页面空间。	
	 display:none	 //因display属性主要是框类型，none 隐藏元素则不会占据原有空间

<!--more-->

以下详细

## 属性
visibility属性规定元素是否可见。<br>
display属性规定应该生成的框的类型。<br>

## 特性
都可以显示隐藏元素。<br>
### [visibillity](http://www.w3school.com.cn/cssref/pr_class_visibility.asp)

属性 | 解释
-------|-------
visibility | 默认值。元素是可见的
hidden | 元素是不可见的。
collapse | 当在表格元素中使用时，此值可删除一行或一列，但是它不会影响表格的布局。被行或列占据的空间会留给其他内容使用。如果此值被用在其他的元素上，会呈现为 "hidden"。
inherit | 规定应该从父元素继承 visibility 属性的值。

### [display](http://www.w3school.com.cn/cssref/pr_class_display.asp)
属性 | 解释
-------|-------
none | 此元素不会被显示

当然display还有很多属性（可参考[W3school](http://www.w3school.com.cn)最近好像改版了，比原来好看多了），和visibility的区别主要也是可见性。

### DEMO

	<!DOCTYPE html>
	<html lang="en">
	<head>
	<meta charset="UTF-8">
	<title>visibility</title>
	<style type="text/css">
		div{
			width: 100px;
			height: 100px;
			background-color: red;
			margin: 10px;
		}
		#b1{
			
		}
	</style>
	</head>
	<body>
		<div id="b1">1</div>
		<div>2</div>
	</body>
	</html>


![](http://120.77.32.127/ty_home/blogImg/2017060201.png)
### visibility

	#b1{
		visibility:hidden;
	}

![](http://120.77.32.127/ty_home//blogImg/2017060202.png)
### display

	#b1{
		display:none;
	}

![](http://120.77.32.127/ty_home//blogImg/2017060203.png)

感谢：）