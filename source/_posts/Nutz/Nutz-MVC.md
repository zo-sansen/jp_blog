---
title: Nutz-MVC
date: 2019-3-21
author: alanJiang
tags:
    - Nutz
categories:
    - Nutz
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: Nutz模式学习记录
---
# 请求流程
![nutz_mvc_workflow_overview.png](/img/other/nutz_mvc_workflow_overview.png)

<qq>任何一个请求都会经过四道工序</qq>
- 过滤器：你通过 @Filters 注解可以为你的入口函数定义任意多的过滤器
- 适配器：http流转换成入口参数
- 调用入口函数
- 处理入口函数的返回类型








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
