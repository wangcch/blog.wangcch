---
title: vuex 简单案例
date: 2018-03-23
categories:
- js
- Vue
tags:
- Vue
- js
- vuex
---

Vuex 是专门为 Vue.js 设计的状态管理库，以利用 Vue.js 的细粒度数据响应机制来进行高效的状态更新。
<!-- more -->

## Vuex 是什么
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。（我浅显的理解为全局状态变量）
> 官方中文文档：[https://vuex.vuejs.org/zh-cn/](https://vuex.vuejs.org/zh-cn/)

![vuex](https://vuex.vuejs.org/zh-cn/images/vuex.png)

## 为什么使用

还是对**全局变量的需求，实现数据状态的跨组件双向绑定**。一两个变量需求vue api props 还是可以实现的，虽然比较麻烦。但是如果状态增加，使用组件的数目变多，那props是很可怕了...所以一般情况还是很有必要使用vuex

Vuex确实让我很头痛，看文档不是很理解，最近才有点收获，记录一下。看文档是一方面，真正理解还是需要自己动手实验一遍。

> 官方推荐：
虽然 Vuex 可以帮助我们管理共享状态，但也附带了更多的概念和框架。这需要对短期和长期效益进行权衡。
如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。确实是如此——如果您的应用够简单，您最好不要使用 Vuex。但是，如果您需要构建是一个中大型单页应用，您很可能会考虑如何更好地在组件外部管理状态，Vuex 将会成为自然而然的选择

> Dan Abramov : Flux 架构就像眼镜：您自会知道什么时候需要它。

## 核心概念

||||
|--|--|--|
|State|单一状态树|（状态存储）|
|Getter|计算属性|（获取）|
|Mutation|事件注册|（状态更改的地方）|
|Action|事件注册|（调用mutation，不能直接改变状态）|
|Module|模块|（组件模块化，拥有完整的事件）|

## DEMO
直接上案例
```js
// store/index.js

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

// 单一状态
const state = {
  isOpen: false,
  statusDemo: 'demo'
}

// 事件注册
const mutations = {
  open (state) {
    state.isOpen = true
  },
  
  close (state) {
    state.isOpen  = false
  }

  changeStatus (state, data) {
    state.statusDemo = data
  }
}

// 事件注册调用、处理
const actions = {
  setOpen: ({ commit }) => commit('open'),
  setClose: ({ commit }) => commit('close'),
  
  // 传参 DEMO
  setStatus ({ commit }, data) {
    commit('changeStatus', data)
  }
}

// 计算属性 状态处理
const getters = {
  getIsOpen: state => state.isOpen,
  getStatusDemo: state => state.statusDemo
}

export default new Vuex.Store({
  state,
  mutations,
  actions,
  getters
})
```

### 调用
```js
// Demo.vue
<script>
import { mapGetters, mapActions } from 'vuex'
export default {
    name: 'demo',
    data () {
        return {}
    },
    
    computed: {
        ...mapGetters([
            'getIsOpen',
            'getStatusDemo'
        ])
    },
    
    methods: {
        ...mapActions([
            'setOpen',
            'setClose',
            'setStatus'
        ]),
        
        demo () {
            // 调用
            console.log(this.getIsOpen, this.getStatusDemo)
            this.setOpen()
            // 调用（传参）
            this.setStatus('demo')
        }
    }
}

</script>
```