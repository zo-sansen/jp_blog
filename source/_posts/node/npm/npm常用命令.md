---
title: npm添加依赖
date: 2019-2-13
author: alanJiang
tags:
    - Node
    - npm
categories:
    - Node
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: npm添加依赖
---
# 安装模块（npm install）[参考](http://www.cnblogs.com/PeunZhang/p/5553574.html)
```
npm install --save vue-router vuex
npm install --save-dev stylus-loader babel-runtime
```


# npm下载太慢
```
>npm install --registry=https://registry.npm.taobao.org
```
# 配置淘宝源
```
全局设置下载源：
npm config set registry https://npm.taobao.org/mirrors/node

下载node源码加速：
npm config set disturl https://npm.taobao.org/mirrors/node 

手动修改配置文件
npm config edit
```
