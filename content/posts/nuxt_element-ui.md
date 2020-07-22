---
title: Nuxt element-ui
date: 2018-04-12
categories:
- js
- Vue
tags:
- js
- Vue
- Nuxt
- element
---
Nuxt 引入js插件 以element-ui 为例
<!--more-->

## nuxt.config.js
> 可以通过[nuxt.config.js](https://zh.nuxtjs.org/guide/configuration) 覆盖Nuxt默认配置

坑点：**theme-chalk**。google搜了一下，theme-default（看了下帖子时间2016年？）。其实主要还是去/node_modules/element-ui/lib/... 下自己看下

```js
// nuxt.config.js

// 生成的 vendor.bundle.js 文件中新模块，以减少应用 bundle 的体积
vender:[
   'element-ui'
],

//  配置使用 Vue.js 插件。
plugins: [
  { src: '~plugins/element-ui', ssr: true }
],
css: [
  // element样式全局引用
  'element-ui/lib/theme-chalk/index.css'
]
  
```

element-ui 搭配插件按需引入组件主题
```js
// nuxt.config.js

babel:{
  "plugins": [["component", [
    {
      "libraryName": "element-ui",
      "styleLibraryName": "theme-chalk"
    },
    'transform-async-to-generator',
    'transform-runtime'
  ]]],
  comments: true
}
```
## plugins
> Nuxt 插件目录 ([plugins](https://zh.nuxtjs.org/guide/plugins))

新建element-ui.js文件
```js
// plugins/element-ui.js

import Vue from 'vue'
import Element from 'element-ui'
Vue.use(Element)
```