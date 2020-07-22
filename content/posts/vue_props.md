---
title: Vue Props
date: 2018-05-20
categories:
- Vue
tags:
- Vue
---
> Prop 是你可以在组件上注册的一些自定义特性。当一个值传递给一个 prop 特性的时候，它就变成了那个组件实例的一个属性。

<!--more-->

简单来说就是：可以**通过Prop向子组件传递数据**。

为什么使用？项目组件化，实现实现自定义组件的高度复用性与自定义化。

## DEMO

```vue
// Page.vue
<template>
  <div class="page-demo">
    <props-demo :data="demo"></props-demo> // prop 传值
  </div>
</template>
<script>
import PropsDemo from '~/components/PropsDemo.vue'

export default {
  name: 'page-demo',
  data () {
    return {
      demo: 'hello'
    }
  },
  components: {
    PropsDemo
  }
}
</script>
```

```vue
// PropsDemo.vue

<template>
  <div class="props-demo">
    <p>{{ demo }}</p>
  </div>
</template>

<script>
export default {
  name: "props-demo",
  props: ['demo']
};
</script>
```

## props验证

```js
props: {
  // 类型检测 默认任何类型自动匹配
  prop1: Number,
   
  // 多种类型
  prop2: [String, Number],
   
  // 必传且是字符串
  prop3: {
    type: String,
    required: true
  },
   
  // (数字) 默认值
  prop4: {
    type: Number,
    default: 0
  },
   
  // 自定义验证函数
  prop5: {
    validator: function (value) {
      return value > 0
    }
  }
}

```

## 双向绑定
props主要用于数值的单项传递，但能否实现双向传值绑定呢？是的，他也可以。就是比较麻烦，个人不推荐

下面看案例：

```vue
// Father.vue
<template>
  <div class="father">
    <p>{{ demo }}</p>
    <child-demo :data="demo" @change-prop="changeProp"></child-demo>
  </div>
</template>
<script>
import ChildDemo from '~/components/ChildDemo.vue'

export default {
  name: 'father',
  data () {
    return {
      demo: true
    }
  },
  
  methods: {
    // 子组件（ChildDemo.vue）的值发生变化，
    // 父组件（Father.vue）相对的值也会发生变化
    changeProp (val) {
      this.demo = val
    }
  },

  components: {
    ChildDemo
  }
}
</script>
```

```vue
// ChildDemo.vue

<template>
  <div class="child-demo">
    <p>{{ demo }}</p>
    <button @click="changeData">change</button>
  </div>
</template>

<script>
export default {
  name: "child-demo",
  props: ['demo'],
  
  methods: {
    changeData () {
      this.changeDemo(!this.demo)
    },
    
    changeDemo (val) {
      this.$emit('change-prop', val)
    }
  },
  
  watch: {
    // 监听 demo 的值变化
    demo (val) {
      this.$emit('change-prop', val)
    }
  },
};
</script>
```