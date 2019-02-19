---
title: （1）vue项目初始化
date: 2019-2-13
author: alanJiang
tags:
    - VUE
categories:
    - VUE
thumbnail:  /img/other/vue-components.svg
blogexcerpt: 利用vue-cli+webpack工具创建中大型vue项目
---
# init[参考](https://segmentfault.com/a/1190000004706690) [大型vue项目](https://www.ctolib.com/PanJiaChen-vue-element-admin.html)
```vue
npm install -g vue-cli
vue init webpack demo
cd demo
npm install
```
创建完的目录结构
![alt]("/img/other/webwxgetmsgimg (2).jpeg")

# 目录详解
- <t>build</t>：目录是一些webpack的文件，配置参数什么的，一般不用动
- <t>src</t>：项目开发相关源码
- <t>static</t>：生成好的文件会放在这个目录下。
- <t>test</t>：测试文件夹，测试都写在这里
- <t>.babelrc</t>： babel编译参数，vue开发需要babel编译
- <t>.editorconfig</t>：不知名开发工具配置文件
- <t>.eslintrc.js</t>： eslint配置文件，用以规范团队开发编码规范，大中型项目很有用
- <t>.gitignore</t>：git过滤配置
- <t>index.html</t>：主页
- <t>package.json</t>： 项目文件，记载着一些命令和依赖还有简要的项目描述信息

# 项目添加依赖引用
```vue
npm install --save vue-router vuex
npm install --save-dev stylus-loader babel-runtime
```
## 模块简介
### vue-router
vue-router用起来非常的简单
入口文件(<t>src/main.js</t>)：

{% raw %}
<style>

t{
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
 
</style>
{% endraw %}
