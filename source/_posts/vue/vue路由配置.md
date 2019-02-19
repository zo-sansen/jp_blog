---
title: vue路由配置
date: 2019-2-7
author: alanJiang
tags:
    - VUE
categories:
    - VUE
thumbnail:  /img/other/vue-components.svg
blogexcerpt: vue路由配置
# vue-router核心功能
---
- 嵌套路由/视图映射
- 模块化，基于组件的路由器配置
- 路线参数，查询，通配符
- 查看由Vue.js过渡系统提供支持的过渡效果
- 细粒度的导航控制
- 与自动活动CSS类的链接
- HTML5历史模式或散列模式，在IE9中具有自动回退功能
- 可自定义的滚动行为

# 全局访问 Vue.$router

# url匹配
## 路由入门配置
```javascript 1.6
routes: [
    // dynamic segments start with a colon
    { path: '/user/:id', component: User }
  ]
```
- ‘:’:动态段，this.$route.params中的参数同名，传参方式
```html
<div>User {{ $route.params.id }}</div>
```
举例：
path|编译path|$route.params
:-|:-|:-
/user/:username|/user/evan|{ username: 'evan' }
/user/:username/post/:post_id|/user/evan/post/123|{ username: 'evan', post_id: '123' }

- <t>/</t>:表示路由路径，视为根路径，不写<t>/</t>,视为相对路径
- <t>*</t>:表示所有路由，事例：<t>path: '*'</t> <t>path: '/user-*'</t> 
- <t>优先级</t>：有时，多个路由可以匹配相同的URL。在这种情况下，匹配优先级由路由定义的顺序确定：路由定义越早，它获得的优先级越高。

## 嵌套路由
```
/user/foo/profile                     /user/foo/posts
+------------------+                  +-----------------+
| User             |                  | User            |
| +--------------+ |                  | +-------------+ |
| | Profile      | |  +------------>  | | Posts       | |
| |              | |                  | |             | |
| +--------------+ |                  | +-------------+ |
+------------------+                  +-----------------+
```

### 嵌套路由上一级组件
<router-view></router-view>:子路由展示标签

<t>定义</t>
```ecmascript 6
{ 
    path: '/user/:id',//路由地址
    component:User,//路由地址对应页面组件
    children:[//子路由
        {
          path: 'profile',
          component: UserProfile
        },
        {
          path: 'posts',
          component: UserPosts
        }
    ]
}
```

### 命名视图
```html
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>
```
```ecmascript 6
routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]
```
### 重定向
重定向到请求路径
```ecmascript 6
routes: [
    { path: '/a', redirect: '/b' }
]
```
重定向到请求配置路径
```ecmascript 6
routes: [
    { path: '/a', redirect: { name: 'foo' }}
]
```
使用函数进行动态重定向
```ecmascript 6
{ path: '/a', redirect: to => {
      // the function receives the target route as the argument
      // return redirect path/location here.
    }}
```
### 别名
可以通过访问<t>/a</t>访问到<t>/b</t>,并且<t>/b</t>依然存在
routes: [
    { path: '/a', component: A, alias: '/b' }
  ]

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
