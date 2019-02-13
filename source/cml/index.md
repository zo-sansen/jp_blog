---
title: 滴滴全平台框架Chameleon
date: 2019-2-11
author: alanJiang
tags:
    - Chameleon
categories:
    - Chameleon
thumbnail: /img/gitee/100_100.png
blogexcerpt: 滴滴全平台框架Chameleon学习使用
---
## 官方文档
[官方文档](https://cmljs.org/doc/component/component.html)

## 常用命令
> npm i -g chameleon-tool
> 全局安装chameleon工具

> cml -v
> cml -h

> cml init project
> 创建项目与启动

> cml dev
> 创建项目与启动

> cml init page
> 创建新页面

>       cml init component
>       first-com
> 创建及引用组件

>       <template>
>         <view>
>            <first-com></first-com>
>          </view>
>        </template>

---

## 架构
### 目录结构
>       ├── chameleon.config.js                 // 项目的配置文件
>       ├── dist                                // 打包产出目录
>       ├── mock                                // 模拟数据目录
>       ├── node_modules                        // npm包依赖
>       ├── package.json
>       └── src                                 // 项目源代码
>           ├── app                             // app启动入口
>           ├── components                      // 组件文件夹
>           ├── pages                           // 页面文件夹
>           ├── router.config.json              // 路由配置文件
>           └── store                           // 全局状态管理
        

### 路由
在router.config.json文件中配置

### 属性
#### 属性类型
    类型	描述	注解
    String	字符串	`"string"`
    Number	数字	`1, 1.5`
    Boolean	布尔值	`true，false`
    Array	数组	`[1, 'string']`
    Object	对象	`{key: value}`
    EventHandler	事件处理函数名	`handlerName`是组件中定义的事件处理函数名
    
#### 公共属性
    属性名	类型	描述	注解
    id	String	组件唯一标示	保证整个页面唯一
    class	String	组件样式类名	在cmss中定义的样式类
    style	String	组件内联样式	可动态设置内联样式
    c-bind	EventHandler	组件事件	

### 视图层
视图层由 CML 与 CMSS 编写

#### CMSS
`cmss写在.cml文件中的<style>标签内`

##### class
###### 静态class
```
<view class="kind-list-item-hd-show class2 class3"></view>
```

###### 动态class
```
目前 class 不支持传入对象的形式； 简单数据绑定 {{}}之内的会被当做一个表达式去处理；

<view><text class="\{\{prefix+'a'\}\}">class数据绑定</text></view>
<script>
class Index {
  data () {
    return {
      prefix: 'cls'
    }
  }
}
export default new Index();
</script>
```
        
###### 三元运算符
```
<view class="static" class="\{\{open ? 'cls1 cls2' : 'cls3 cls4'\}\}">
</view>
 ```   

##### 布局
> 与css差不多

##### 盒子模型
> 与css差不多

##### 样式的多态
cml在不同平台的样式

    <style>
    @media cml-type (支持的平台) {
    
    }
    .common {
      /**/
    }
    <style>

类型有:
>   - web
>   - weex
>   - wx
>   - alipay
>   - baidu

例如:
>   @media cml-type (web) {
      .class1 {
        color: red;
      }
    }

因为多态只能在cml文件中使用,如果想使用在.css文件中,如果需要使用其他文件中引用进来,可以:

    <style lang="less">
    @media cml-type (web) {
      @import "./style1.less";
    }
    @media cml-type (weex) {
      @import "./style2.less";
    
    }
    @media cml-type (wx,alipay,baidu) {
      @import "./style3.less";
    }
    </style>
    
    
    
#### CML-标准语法

#### CML-类VUE语法
>   模板添加一个lang属性<template lang="vue">

### 逻辑层
#### 生命周期
钩子|执行时机|详细
:-|:-|:-
beforeCreate|实例初始化之后，数据和方法挂在到实例之前 一个页面只会返回一次|在该生命周期回调函数中会返回传入当前页面的参数对象
created|	数据及方法挂载完成|
beforeMount|开始挂载已经编译完成的cml到对应的节点时|
mounted|cml模板编译完成,且渲染到dom中完成|
beforeDestroy|实例销毁之前|
destroyed|	实例销毁后|
#### 计算属性computed
> 就是一个方法,可以对一个值,或者进行逻辑处理之后,再返回给页面
```
<text>Computed reversed message: "{{ reversedMessage }}"</text>

class Index {
  data = {
    message: 'Hello'
  }
  computed = {
    // 计算属性的 getter
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  }
};
export default new Index();
```
#### 侦听属性 watch
```
<text>fullName is : "{{ fullName }}"</text>
class Index {
  data = {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  }
  watch = {
    firstName: function (newV, oldV) {
      this.fullName = newV + ' ' + this.lastName
    },
    lastName: function (newV, oldV) {
      this.fullName = this.firstName + ' ' + newV
    }
  }
};
export default new Index();
```
#### 数据管理
>   chameleon-store 提供集中管理数据的能力。

- state
- getters
- mutation
- action
- 子模块

##### 简单开始
1. 创建 store，并且提供一个初始 state 对象和一些 mutation：
```
import createStore from 'chameleon-store'
const store = createStore({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
export default store
```
2. 通过 store.state 来获取状态对象，以及通过 store.commit 方法触发状态变更：
```
store.commit('increment')

console.log(store.state.count) // -> 1
```
---
### 配置
针对项目、组件、路由等的特定配置，以满足各种方式的需求

#### 组件配置
组件的配置以json对象的格式配置在.cml文件中，结构如下：

#### 路由配置
chameleon项目内置了一套各端统一的路由管理方式

`src/router.config.json是路由的配置文件,内容如下：`

```
  "mode": "history",
  "domain": "https://www.chameleon.com",
  "routes":[
    {
      "url": "/cml/h5/index",
      "path": "/pages/index/index",
      "mock": "index.php"
    }
  ]
}
```
- mode 为web端路由模式，分为hash或history。
- domain 为web端地址的域名。
- routes 为路由配置
    - path为路由对应的cml文件的路径,以src目录下开始的绝对路径，以/开头。
    - url为web端的访问路径。
    - mock为该路由对应的mock文件(仅模拟模板下发需要)。
#### 项目配置
本文档描述了项目配置的全部参数及使用方法。
chameleon的构建过程是配置化的，项目的根目录下提供一个chameleon.config.js文件，在该文件中可以使用全局对象cml的api去操作配置对象。例如：