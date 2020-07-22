---
title: HTML 移动前端viewport
date: 2017-06-05
categories:
- HTML
tags:
- HTML
- viewport
---

在开发响应式网站时[Wangcch's CV]('http://cv.theyear.space')，并未在移动窗口进行测试。结果在服务器部署测试时手机并没有自适应窗口，只是显示网页缩放版本。后来查资料，一行代码解决...

	<meta name="viewport" content="width=device-width,
	 initial-scale=1.0, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0"/> 

<!--more-->

## viewport概念
viewport:视口，视觉窗口，显示区域。viewport是用户网页的可视区域。手机浏览器是把页面放在一个虚拟的"窗口"（viewport）中，通常这个虚拟的"窗口"（viewport）比屏幕宽，这样就不用把每个网页挤到很小的窗口中（这样会破坏没有针对手机浏览器优化的网页的布局），用户可以通过平移和缩放来看网页的不同部分。

1. layout viewport(布局视口)
一般为移动设备浏览器默认设置了一个viewport原标签，定义一个虚拟的layout view(布局视口)，使pc上面的网页基本能在手机上呈现，一般模式支持手动缩放网页。

2. visual viewport(视觉视口)
visual viewport（视觉视口）备物理屏幕的可视区域，屏幕显示器的物理像素，同样尺寸的屏幕，像素密度大的设备，硬件像素会更多。

3. ideal viewpore(理想视口)
ideal viewport（理想视口）通常是屏幕分辨率.
dip （设备逻辑像素）跟设备的硬件像素无关的。一个 dip 在任意像素密度的设备屏幕上都占据相同的空间。页面通过逻辑像素显示。<br>
逻辑像素宽度*倍率 = 物理像素宽度<br>
不同设备的倍率一般不同，更多设备ideal viewport可以查看[viewportsizes](http://viewportsizes.com/)


## CSS像素
CSS像素（px）用于页面布局的单位。样式的像素尺寸（例如 width: 100px）是以CSS像素为单位指定的。CSS像素与 dip 的比例即为网页的缩放比例，如果网页没有缩放，那么一个CSS像素就对应一个 dip（设备逻辑像素）。

## 利用meta标签对viewport进行控制

	<meta name="viewport" content="width=device-width,
	 initial-scale=1.0, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0"/>

属性名 | 取值 | 描述
--------|-------|-------
width | 正整数 或 device-width | 定义视口窗口的宽度，单位为像素
height | 正整数 或 device-height	| 定义视口的高度，单位为像素，一般不用
initial-scale | [0.0-10.0]	| 定义初始缩放值
minimum-scale | [0.0-10.0]	| 定义缩小最小比例，它必须小于或等于maximum-scale设置
maximum-scale | [0.0-10.0] | 定义放大最大比例，它必须大于或等于minimum-scale设置
user-scalable | yes/no | 定义是否允许用户手动缩放页面，默认值yes

设置viewport布局视口，宽度为设备宽度，禁止用户缩放，默认显示无缩放显示（即为1.0倍数）。

感谢:)