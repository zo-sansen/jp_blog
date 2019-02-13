---
title: vue路由跳转
date: 2019-2-7
author: alanJiang
tags:
    - VUE
categories:
    - VUE
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: vue路由跳转使用
---
# 1.router-link跳转

```// 直接写上跳转的地址
      <router-link to="/detail/one">
        <span class="spanfour" >link跳转</span>
      </router-link>
      // 添加参数
      <router-link :to="{path:'/detail/two', query:{id:1，name:'vue'}}">
       </router-link>
      // 参数获取
      id = this.$route.query.id
      // 新窗口打开
      <router-link :to="{path:'/detail/three', query:{id:1，name:'vue'}}" target="_blank">
      </router-link>
```
--------------------- 

# 2.this.$router.push跳转
```toDeail (e) {
      this.$router.push({path: "/detail", query: {id: e}})
    }
    // 参数获取
    id = this.$route.query.id
    
    toDeail (e) {
      this.$router.push({name: "/detail", params: {id: e}})
    }
    // 注意地址需写在 name后面
    //参数获取，params和query区别，query参数在地址栏显示，params的参数不在地址栏显示
    id = this.$route.params.id
```
--------------------- 
# 3..this.$router.replace跳转
```
//和push的区别，push有记录一个history，replace没有
 toDeail (e) {
   this.$router.replace({name: '/detail', params: {id: e}})
 }

4. resolve跳转
  resolve页面跳转可用新页面打开
 2.1.0版本后，使用路由对象的resolve方法解析路由，可以得到location、router、href等目标路由的信息。得到href就可以使用window.open开新窗口了（这边应用：https://segmentfault.com/q/1010000009557100下的一个回答）
 toDeail (e) {
   const new = this.$router.resolve({name: '/detail', params: {id: e}})
   window.open(new.href,'_blank')
 }```
--------------------- 