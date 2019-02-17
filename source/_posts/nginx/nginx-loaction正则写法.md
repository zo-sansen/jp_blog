---
title: nginx-loaction正则写法
date: 2019-2-18
author: alanJiang
tags:
    - Nginx
categories:
    - Nginx
thumbnail:  \img\nginx\bg2018022701.png
blogexcerpt: nginx-loaction正则写法
---
精确匹配

    location  = / {
      # 精确匹配 / ，主机名后面不能带任何字符串
      [ configuration A ] 
    }
    同样的
    但是正则和最长字符串会优先匹配

    location  / {
      # 因为所有的地址都以 / 开头，所以这条规则将匹配到所有请求
      [ configuration B ] 
    }
    
    location /documents/ {
      # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
      # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
      [ configuration C ] 
    } 
    location ~ /documents/Abc {
      # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
      # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
      [ configuration CC ] 
    }
    location ^~ /images/ {
      # 匹配任何以 /images/ 开头的地址，匹配符合以后，停止往下搜索正则，采用这一条。
      [ configuration D ] 
    }
<qq>参解</qq>
- 已<qq>=</qq>开头表示精确匹配
  如 A 中只匹配根目录结尾的请求，后面不能带任何字符串。
- <qq>^~</qq> 开头表示uri以某个常规字符串开头，不是正则匹配
- <qq>~</qq> 开头表示区分大小写的正则匹配;
- <qq>~*</qq> 开头表示不区分大小写的正则匹配;
- <qq>/</qq> 通用匹配, 如果没有其它匹配,任何请求都会匹配到

<qq>顺序 no优先级：</qq>
(location =) > (location 完整路径) > (location ^~ 路径) > (location ~,~* 正则顺序) > (location 部分起始路径) > (/)


[推荐地址](https://segmentfault.com/a/1190000002797606)

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