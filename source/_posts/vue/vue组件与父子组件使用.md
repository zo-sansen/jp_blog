---
title: vue组件与父子组件使用
date: 2019-2-13
author: alanJiang
tags:
    - VUE
categories:
    - VUE
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: 学习使用vue组件与父子组件，组件的通讯，引用，传参，方法调用等
---

# component(组件)
## 直接写法
```
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
```

## 组件注册
### 组件名
定义组件名的方式有两种
#### 使用 kebab-case
>   Vue.component('my-component-name', { /* ... */ })
#### 使用 PascalCase
>   Vue.component('MyComponentName', { /* ... */ })

<p style="color:red">直接在 DOM (即非字符串的模板) 中使用时只有 kebab-case 是有效的</p>

### 全局注册
```Vue.component('my-component-name', {
     // ... 选项 ...
   })
```
<p style="color:red">这些组件是全局注册的。也就是说它们在注册之后可以用在任何新创建的 Vue 根实例</p>
 
### 局部注册
普通注册
```new Vue({
     el: '#app',
     components: {
       'component-a': ComponentA,
       'component-b': ComponentB
     }
   })

```
组件内组件注册
```
var ComponentA = { /* ... */ }

var ComponentB = {
  components: {
    'component-a': ComponentA
  },
  // ...
}
```

### 模块系统
#### 在模块系统中局部注册
假设的 ComponentB.js 或 ComponentB.vue 文件中：
```$xslt
import ComponentA from './ComponentA'
import ComponentC from './ComponentC'

export default {
  components: {
    ComponentA,
    ComponentC
  },
  // ...
}
```
现在 ComponentA 和 ComponentC 都可以在 ComponentB 的模板中使用了。

#### 基础组件的自动化全局注册

```$xslt
import BaseButton from './BaseButton.vue'
import BaseIcon from './BaseIcon.vue'
import BaseInput from './BaseInput.vue'

export default {
  components: {
    BaseButton,
    BaseIcon,
    BaseInput
  }
}
```

可以使用webpack，`require.context`只全局注册这些非常通用的基础组件

```$xslt
import Vue from 'vue'
import upperFirst from 'lodash/upperFirst'
import camelCase from 'lodash/camelCase'

const requireComponent = require.context(
  // 其组件目录的相对路径
  './components',
  // 是否查询其子目录
  false,
  // 匹配基础组件文件名的正则表达式
  /Base[A-Z]\w+\.(vue|js)$/
)

requireComponent.keys().forEach(fileName => {
  // 获取组件配置
  const componentConfig = requireComponent(fileName)

  // 获取组件的 PascalCase 命名
  const componentName = upperFirst(
    camelCase(
      // 剥去文件名开头的 `./` 和结尾的扩展名
      fileName.replace(/^\.\/(.*)\.\w+$/, '$1')
    )
  )

  // 全局注册组件
  Vue.component(
    componentName,
    // 如果这个组件选项是通过 `export default` 导出的，
    // 那么就会优先使用 `.default`，
    // 否则回退到使用模块的根。
    componentConfig.default || componentConfig
  )
})
```
<p style="color:red">记住全局注册的行为必须在根 Vue 实例 (通过 new Vue) 创建之前发生。这里有一个真实项目情景下的示例。</p>

[require.context详解](www.baidu.com)


# 子组件使用父组件
关键字
- $parent：

- prop：单向数据流传递，向下传递，

子组件定义
`props: ['initialCounter'],`

父组件引用
>   单个传
>   <blog-post v-bind:initialCounter="post.author"></blog-post>

>   传入一个对象的所有属性
```$xslt
post: {
  id: 1,
  title: 'My Journey with Vue'
}
```
模板使用方式：
```$xslt
<blog-post v-bind="post"></blog-post>
等于
<blog-post
  v-bind:id="post.id"
  v-bind:title="post.title"
></blog-post>
```

## 依赖注入方式
- provide：允许我们指定我们想要提供给后代组件的数据/方法
 
    例子：
```
provide: function () {
             return {
               getMap: this.getMap
             }
           }
```

- inject：来接收指定的我们想要添加在这个实例上的属性

`inject: ['getMap']`