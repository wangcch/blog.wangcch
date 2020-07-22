---
title: js 循环延时踩坑
date: 2018-01-24
categories:
- js
tags:
- js
---

为什么遇到循环延时操作了。一切源于在小程序开发过程中循环生成多个二维码事件，二维码画图太慢，在读取canvas画图地址时，不给一定盾延时是无法读取到图片地址的。再加上小程序不支持多线程。画图需要一定的时间，又处于占用时期。基本情况就是能生成第一个二维码，之后都读取不到地址。

<!-- more -->

---
## Before

```js
// 事例
for (let id in data) {
    console.log(id);
    this.createQr(id, content); // 生成二维码
}
```
基本输出：
```
0
1
2
...
{ createQr() 输出结果  }
```
可以看出循环很快结束，createQr()的执行结果在循环log之后。

> for 循环会快速遍历data数组，又是单线程，最后id=0之后的createQr()都是失败的。所以希望能都等一会，再循环下一个。

## Next
想试试加个延时看看
```js 
for (let id in data) {
    setTimeout( () => {
        console.log(id);
        this.createQr(id, content);
    }, 1000); 
}
```
基本输出：
```
n
n
n 
...
// 等待了 1s
{ createQr() 输出结果  }
```

可以知道还是循环先执行，1s之后已经是最后一个id了。所以延时不能添加到for循环里。

## And Next
createQr() 中添加延时试试
```js 
for (let id in data) {
    console.log(id);
    this.createQr(id, content);
}

creatQr: function (id, content) {
    setTimeout( () => {
        // DO
    }, 1000); 
}
```
基本输出：
```
0
1
2 
...
// 等待了 1s
{ createQr() 输出结果  }
```
是不是感觉又回到了起点？

实际情况是：等于for循环同时调用data.length个createQr(); 等待1s在执行createQr()内的内容。由于单线程，又只是执行了一个。

其实我们想的不过就是第1s: ->createQr() ; 第2s: ->create() ; 第3s: ->create() ; ...... 所以我需要 ** 梯度延时 **

## Now
```js 
for (let id in data) {
    console.log(id);
    this.createQr(id, content);
}

creatQr: function (id, content) {
    setTimeout( () => {
        // DO
    }, id*1000);  // 延时叠加
}
```
基本输出：
```
0
1
2 
...
// 等待了 1s
{ createQr() 输出结果  }
// 等待了 1s
{ createQr() 输出结果  }
// 等待了 1s
{ createQr() 输出结果  }
...
```
现在基本上算是解决了画图延时带来的问题。