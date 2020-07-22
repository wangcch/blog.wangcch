---
title: 自定义 input>radio 单选
date: 2018-06-07
categories:
- CSS
tags:
- CSS
- radio
- checkbox
---

自定义radio/checkbox 单选/多选样式，原理都是一样的

```html
<input type="radio" />
<input type="checkbox" />
```
<!-- more -->

## 前言

是在写个react练手项目[react-todo](https://github.com/wangcch/react-todo)中选择状态（all、active、completed）的选中表示。开始也是准备添加格外的css属性来表示选中状态。js判断是谁高亮，但总感觉这种方法很笨，组件化显得很重，不够灵活。因为没有路由分页处理不同筛选（all、active、completed），所以说白了，这就是一个radio选中，只是自己把事情想麻烦了。
当然，默认的input>radio肯定不是我们想要的，所以我们不妨修改一下。

![image](https://cdn.wangcch.cc/blog/20180607151150.png)

## DEMO

原理很简单：**label关联，再隐藏原来的input>radio**。

```html
<div class="radio-box">
    <label class="radio-item">
        <input type="radio" name="filter" id="demo1" value="demo1" hidden />
        <span class="radio-item_name">demo1</span>
    </label>
    <label class="radio-item">
        <input type="radio" name="filter" id="demo2" value="demo2" hidden />
        <span class="radio-item_name">demo2</span>
    </label>
    <label class="radio-item">
        <input type="radio" name="filter" id="demo3" value="demo3" hidden />
        <span class="radio-item_name">demo3</span>
    </label>
</div>
```

```css
.radio-box {
	max-width: 500px;
	margin: 30px auto;
  border-radius: 3px;
  padding: 10px 12px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.06) inset;
  border: 1px solid #f5f5f5;
  display: flex;
  justify-content: center;
  align-items: center;
}

.radio-box .radio-item {
  flex: 1;
  text-align: center;
}

.radio-box .radio-item .radio-item_name {
  padding: 2px 10px;
  font-size: 12px;
  color: #909399;
  font-weight: bold;
  cursor: pointer;
}

.radio-box .radio-item input[type="radio"]:checked+.radio-item_name {
  border: 1px solid #f5f5f5;
  border-radius: 3px;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.06);
}
```

## React Demo

[react-todo/src/todoFilter.js](https://github.com/wangcch/react-todo/blob/master/src/todoFilter.js)

## checkbox

既然单选可以，那多选 input>checkbox 也是一样的道理
```html
<label class="check">
  <input type="checkbox" className="check_inout" hidden/>
  <span className="check_dot"></span>
</label>
```

```css
.check {
  cursor: pointer;
}
.check .check_dot {
  position: relative;
  display: inline-block;
  box-sizing: border-box;
  width: 18px;
  height: 18px;
  border: 1px solid #e8e8e8;
  border-radius: 3px;
}
.check input[type="checkbox"]:checked+.check_dot::before {
  position: absolute;
  content: '';
  top: 2px;
  left: 2px;
  border-width: 0 0 2px 2px;
  border-color: #C0C4CC;
  border-style: solid;
  border-radius: 0 0 0 3px;
  width: 16px;
  height: 6px;
  transform: rotate(-30deg);
}
```