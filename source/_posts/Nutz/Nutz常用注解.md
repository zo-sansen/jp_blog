---
title: Nutz常用注解
date: 2019-3-21
author: alanJiang
tags:
    - Nutz
categories:
    - Nutz
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: Nutz常用注解
---
# MVC注解
- @At：入口函数
- @AdaptBy：参数适配器
- @Inject：引用bean
- @Filters：过滤器
    >   注解 '@Filters' 的值是一个 '@By' 注解的数组，它可以声明在这三个地方
     入口函数
     子模块
     主模块
     声明方式：
     @Filters({@By(type=Filter1.class), @By(type=Filter2.class)})
     public final class MainModule{



{% raw %}
<style>
qq {
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
</style>
{% endraw %}
