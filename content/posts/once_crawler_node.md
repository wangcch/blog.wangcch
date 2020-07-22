---
title: node 记一次爬虫
date: 2018-03-01
categories:
- js
- node.js
tags:
- node.js
- cheerio
- fs
- https
---

一直都知道“爬虫”这个名称，但真正手写没试过。主要还是本人懒，再说也没什么需求。但今天因为需要一个测试数据，对着网页[badssl.com](https://badssl.com)，手动敲json文件。真的很多，是在敲不下去，再怎么复制粘贴也受不了。写个爬虫，数据抓取，再格式化输出一下岂不是很棒。我感觉可以。

<!-- more -->

> 依赖： cheerio: 一个nodejs抓取页面模块 [https://github.com/cheeriojs/cheerio](https://github.com/cheeriojs/cheerio)

分几个步骤吧
1. 获取网页数据
2. 数据整理
3. 文件输出

## 获取网页数据

文档：
1. [http](http://nodejs.cn/api/http.html#http_http_get_options_callback)
2. [https](http://nodejs.cn/api/https.html#https_https_get_options_callback)

两个接口服务，更具你抓取的网站条件而定。这里以https为例（http的直接替换<code>https</code>就行了，详细见上方文档）
```js
// getbadssl.js

var https = require('https');

var url = 'https://badssl.com';

https.get(url, function(res) {
  var html = '';
  res.on('data', function(data) {
    html += data;
  });
  res.on('end', function() {
    console.log(html)       // 打印出来会发现这是badssl首页的全部html内容
  });
}).on('error', function() {
  console.log('get error');
});

```

## 数据整理

> 环境构建

```terminal
// 在文件中初始化项目
npm init 

// 安装cheerio
npm install cheerio --save

// 运行getbadssl.js
node getbadssl.js
```
这时文件目录
```
-node_modules
-getbadssl.js
-package-lock.json
-package.json
```

---
回归正题

```js
// getbadssl.js

var https = require('https');
var cheerio = require('cheerio')    // 引入cheerio

var url = 'https://badssl.com';

https.get(url, function(res) {
  var html = '';
  res.on('data', function(data) {
    html += data;
  });
  res.on('end', function() {
    var data = getData(html);      // 传递
  });
}).on('error', function() {
  console.log('get error');
});

// 数据抓取处理
function getData(html) {
  if (html) {
    var $ = cheerio.load(html);     // cheerio
    
    /*
    * 以下数据处理，根据实际的情况而定
    *  
    * 这边化简一下源程序，便于理解，就以抓取 a: url 为例
    */
    var links = $('#links');
    var listData = [];
    links.find('.column').each(function(item) {
      var column = $(this);
      column.find('.group').each(function(index) {
        var group = $(this);
        group.find('a').each(function(id) {
    	  var a = $(this);
    	  var data = {};
    	  data.url = a.attr('href');
    	  data.text = a.html().split('</span>')[1];
    	  listData.push(data);
        })
      });
    });
    var data = {"lists": listData};
    return data;
  } else {
    console.log('null data');
  }
}
```

## 文件输出
既然已经这样了，我们就把抓取到的文件直接输出文件为json文件
> [Node.js 文件系统 fs ](http://nodejs.cn/api/fs.html#fs_fs_writefile_file_data_options_callback)

```js
// 上述 处理数据之后，传给writeFile()输出文件
var data = getData(html);
writeFile(data);
```
```js
function writeFile (data) {
  fs.writeFile('lists.json', JSON.stringify(data, null, "\t"), function(err) {
    if (err) {
      return console.error(err);
    } else {
      console.log('success to ./lists.json')
    }
  })
}
```

我们再次执行<code>node getbadssl.js</code>，我们会发现当前文件夹内多出**lists.json**文件
大致内容如下
```json
// lists.json
{
  "lists": [
  	{
  	  "url": "/dashboard/",
  	  "text": "Dashboard"
  	},
  	{
  	  "url": "https://expired.badssl.com/",
  	  "text": "expired"
  	},
  	{
  	  "url": "https://wrong.host.badssl.com/",
  	  "text": "wrong.host"
  	},
  	{
  	  ...
  	}
  ]
}
```

