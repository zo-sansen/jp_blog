---
title: js Map数据类型操作
date: 2019-2-15
author: alanJiang
tags:
    - JS
    - JS数据类型
categories:
    - JS
thumbnail:  
blogexcerpt: js Map数据类型操作
---

# 遍历map对象
```
var map = [{  
            key : "百度",  
            value : "李彦宏"  },
           {
            key : "阿里巴巴",  
            value : "马云"  },
       ];  

for (var key in map) {  
   console.log(map[key]);  
}
//输出结果
//Object {key : "百度", value : "李彦宏"}
//Object {key : "阿里巴巴", value : "马云"}
```
   
   
# 遍历map集合
```
var m = new Map();
m.set(1, "black");
m.set(2, "red");
m.set("colors", 2);
//方法一：
m.forEach(function (item) {
    console.log(item.toString());
});

//方法二：
m.forEach(function (value, key, map) {
   console.log(value)
})
// 输出:
// black
// red
// 2
//方法三：
for (var [key, value] of m) {
 console.log(key + ' = ' + value);
}
// 输出:
// 1 = black
// 2 = red
// colors  = 2
```
