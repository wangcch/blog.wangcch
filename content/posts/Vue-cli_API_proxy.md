---
title: vue-cli API代理
date: 2018-02-26
categories:
- js
- Vue
tags:
- js
- Vue
---
使用proxyTable进行跨域API代理

<!-- more -->
```js
// config/index.js
module.exports = {
  dev: {
    proxyTable: {
      // 将所有以 /api 开头的请求通过 jsonplaceholder 代理
      '/api': {
        target: 'https://wangcch.cc',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
}
```

调用
```js
this.$http.get('/api/demo').then(function(res){
    console.log(res.data);
})
```
> 依赖
```
npm install vue-resource
```