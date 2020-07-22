---
title: Checkbox自定义menu button
date: 2018-06-17
categories:
- CSS
tags:
- CSS
- checkbox
---

使用 input>checkbox 实现菜单按钮

![css-menu](https://cdn.wangcch.cc/blog/css-menu.gif)

## 前言

记得以前写的这种类似开关都是由点击事件驱动样式（监听点击事件->动态添加样式）。现在看来有点麻烦，不能确定唯一性，单一值驱动相关事件。

自上次总结了 [自定义 radio 单选](https://blog.theyear.space/2018/06/07/custom_radio/) checkbox当然也可以自定义，而且就是一个开关。这样就简单多了，根本无需监听点击事件就可以以 **input>checkbox** 的bool值驱动所有。并且也可以坚定其事件变化。方便～

## 结构

废话不多说，直接上东西

```html
// 框 + 三个横线
<label class="icon-menu">
  <input type="checkbox" hidden>
  <span class="icon-menu_line"></span>
  <span class="icon-menu_line"></span>
  <span class="icon-menu_line"></span>
</label>
```
## 样式

结构上已经隐藏了input>checkbox，所以我们只需添加<code>.icon-menu</code><code>.icon-menu_line</code>样式。

选中状态也可以直接通过<code>input[type="checkbox"]:checked</code>判断，无需事件监听动态修改样式，全css判断

```scss
// font-size: 16px;

.icon-menu {
    position: relative;
    box-sizing: border-box;
    width: 1.5em;
    height: 1.5em;
    border: 2px solid #303133;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    cursor: pointer;
    .icon-menu_line {
        width: 0.75em;
        height: 2px;
        background: #303133;
        display: block;
        margin-top: 2px;
        transition: all 0.2s ease;
        &:nth-of-type(1) {
            margin-top: 0;
        }
    }
    input[type="checkbox"]:checked ~ .icon-menu_line {
        position: absolute;
        margin-top: 0;
        &:nth-of-type(1) {
            transform: rotate(45deg)
        }
        &:nth-of-type(2) {
            display: none;
        }
        &:nth-of-type(3) {
            transform: rotate(-45deg)
        }
    }
}
```

## 事件监听

使用 **checkbox** 就很简单了，直接监听 **input>checkbox** 事件就可以了，没什么麻烦的

### Vue Demo
```html
<label class="icon-menu">
  <input type="checkbox" v-model="isShowMenu" @change="changeShowMenu" hidden>
  <span class="icon-menu_line"></span>
  <span class="icon-menu_line"></span>
  <span class="icon-menu_line"></span>
</label>
```

```js
...
changeShowMenu () {
  console.log(this.isShowMenu)
}
...
```

### React Demo
```jsx
// ...
render() {
    const { data } = this.props;
    return (
      <label className="icon-menu">
        <input type="checkbox" checked={data.checked} onChange={this.props.changeShowMenu} hidden />
        <span className="icon-menu_line" />
        <span className="icon-menu_line" />
        <span className="icon-menu_line" />
      </label>
    );
}
//...
```
