---
title: PWA Manifest
date: 2018-03-21
categories:
- PWA
tags:
- PWA
- manifest
---
## 简介
manifest是一种简单的json 数据风格的配置文件，通过对其相应对属性进行配置，才能实现相应对功能，这里可以称manifest 为WEB应用清单。web应用清单可以实现自定义启动画面、打开url、设置界面颜色、设置桌面图标等等

<!-- more -->

``` json
{
    "short_name": "短名称",
    "name": "这是一个完整名称",
    "icons": [
        {
            "src": "144x144.png",
            "type": "image/png",
            "sizes": "144x144"
        }
    ],
    "background_color": "#2196f3",
    "display": "standalone",
    "start_url": "index.html"
}
```
## 部署到浏览器

``` html
<link rel="manifest" href="manifest.json">
```

## theme_color
    
theme_color: {Color}，定义和background_color一样的CSS颜色值，用于显示Web App的主题色，显示在banner位置。

## description

提供有关Web应用程序的一般描述。
```json
"description": "The PWA"
```

## display

display: {string}，用来指定 Web App 从主屏幕点击启动后的显示类型
|显示类型|描述|降级显示类型|
|-|-|-|
|fullscreen|应用的显示界面将占满整个屏幕|standalone|
|standlone|浏览器相关UI（如导航栏、工具栏等）将会被隐藏|minimal-ui|
|minimal-ui|显示形式与standalone类似，浏览器相关UI会最小化为一个按钮，不同浏览器在实现上略有不同|browser|
|browser|浏览器模式，与普通网页在浏览器中打开的显示一致|（none）|

``` css
@media all and (display-mode: fullscreen) {
    div {
        padding: 0;
    }
}

@media all and (display-mode: standalone) {
    div {
        padding: 1px;
    }
}

@media all and (display-mode: minimal-ui) {
    div {
        padding: 2px;
    }
}

@media all and (display-mode: browser) {
    div {
        padding: 3px;
    }
}
```

## icon

指定可在各种环境中用作应用程序图标的图像对象数组。 例如，它们可以用来在其他应用程序列表中表示Web应用程序，或者将Web应用程序与OS的任务切换器和/或系统偏好集成在一起。

```json
"icons": [
  {
    "src": "icon/lowres.webp",
    "sizes": "48x48",
    "type": "image/webp"
  },
  {
    "src": "icon/lowres",
    "sizes": "48x48"
  },
  {
    "src": "icon/hd_hi.ico",
    "sizes": "72x72 96x96 128x128 256x256"
  },
  {
    "src": "icon/hd_hi.svg",
    "sizes": "72x72"
  }
]
```
|字段|描述|
|--|--|
|sizes|包含空格分隔的图像尺寸的字符串。|
|src|图像文件的路径。 如果src是一个相对URL，则基本URL将是manifest的URL。|
|type|提示图像的媒体类型。此字段的目的是允许用户代理快速忽略不支持的媒体类型的图像。|

## lang

指定**name**和**short_name**成员中的值的主要语言。 该值是包含单个语言标记的字符串。
```
"lang":"en-US"

```
## name
可以理解为全称吧

## short_name
简称，为了在没有足够空间显示Web应用程序的全名时使用。

## orientation

orientation: {string}，Web App的在屏幕上的显示方向。

- landscape-primary，当视窗宽度大于高度时，当前应用处于“横屏”状态
- landscape-secondary，landscape-primary的180°方向
- landscape，根据屏幕的方向，自动横屏幕180°切换
- portrait-primary，当视窗宽度小于高度时，当前应用处于“竖屏”状态
- portrait-secondary，portrait-primary的180°方向
- portrait，根据屏幕方向，自动竖屏180°切换
- natural， 根据不同平台的规则，显示为当前平台的0°方向
- any，任意方向切换

## dir

dir: {string}，设置文字的显示方向。 
- ltr，文本显示方向，左到右 
- rtl，文本显示方向，右到左 
- auto，根据系统的方向显示

## related_applications

related_applications: {Array.<AppInfo>}，用于定义对应的原生应用，类似应用安装横幅的形式去推广、引流。

## AppInfo结构： 
- platform: {string}， 应用平台 
- id: {string} 应用id

## prefer_related_applications

prefer_related_applications:{Boolean}，用于设置只允许用户安装原生应用。
