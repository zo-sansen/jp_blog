---
title: 滴滴全平台框架Chameleon API
date: 2019-2-11
author: alanJiang
tags:
    - Chameleon
categories:
    - Chameleon
thumbnail: /img/gitee/100_100.png
blogexcerpt: 滴滴全平台框架Chameleon API相关内容
---
>   import cml from 'chameleon-api'

## 路由导航
### navigateTo
保留当前页面，跳转到应用内的某个页面。
#### 参数
参数名|类型|必填|默认值|说明
:-|:-|:-|:-|:-
path|String|是|无|应用内页面的路径， 路由里面的path值 (用于小程序端)
query|Object|否|无|要传递的参数，可在将进入页面的beforeCreate里面获取
#### 返回值
无
#### 举例
```cml.navigateTo({
     path: '/pages/navigateBack/index',
     query: {
       a: 1,
       b: 'test'
     }
   })
```
### redirectTo
关闭当前页面，跳转到应用内的某个页面
#### 参数
参数名|类型|必填|默认值|说明
:-|:-|:-|:-|:-
path|String|是|无|应用内页面的路径， 路由里面的path值 (用于小程序端)
query|Object|否|无|要传递的参数，可在将进入页面的beforeCreate里面获取
#### 返回值
无
#### 举例
```cml.redirectTo({
     path: '/pages/navigateBack/index',
     query: {
       a: 1,
       b: 'test'
     }
   })
```
### navigateBack
关闭当前页面，返回上一页面
#### 参数
参数名|类型|必填|默认值|说明
:-|:-|:-|:-|:-
backPageNum|Number[负数]|否|-1|要返回的页面级数, 为负数, 默认返回上一页
#### 返回值
无
#### 举例
`cml.navigateBack(-1);`
## 网络请求
### get
#### 参数
参数名|类型|必填|默认值|说明
:-|:-|:-|:-|:-
url|String|是||网络请求地址，如果项目中配置了apiPrefix并且setting中的apiPrefix为true，则添加配置的前缀
data|Object|否||要传的参数，会拼接在请求的url中
header|Object   |否||设置http请求的header
resDataType|String|否|json|设置response的数据类型, 为json时, 会尝试对返回值进行JSON.parse()
setting|Object|{apiPrefix: true, jsonp: false}||自定义了设置，apiPrefix为是否添加chameleon.config.js中设置的apiPrefix; jsonp 为 true 时会发起一个 jsonp 请求
#### 举例
```cml.get({
     url: 'https://cml.com/api/user/1'
   }).then(res => {
     cml.showToast({
       message: JSON.stringify(res),
       duration: 2000
     })
   }, err => {
     cml.showToast({
       message: JSON.stringify(err),
       duration: 2000
     })
   })
```
### post
#### 参数
参数名|类型|必填|默认值|说明
:-|:-|:-|:-|:-
url|String|是||网络请求地址，如果项目中配置了apiPrefix并且setting中的apiPrefix为true，则添加配置的前缀
data|Object|否||要传的参数，会拼接在请求的url中
header|Object   |否||设置http请求的header
contentType|String|否|form|取值：form或json，决定body中data的格式，对应header中content-type为application/x-www-form-urlencoded或application/json
resDataType|String|否|json|设置response的数据类型, 为json时, 会尝试对返回值进行JSON.parse()
#### 举例
```cml.post({
     url: 'https://cml.com/api/user/update',
     data: {
       a: 1
     }
   }).then(res => {
     cml.showToast({
       message: JSON.stringify(res),
       duration: 2000
     })
   }, err => {
     cml.showToast({
       message: JSON.stringify(err),
       duration: 2000
     })
   })
```
### request
#### 参数
参数名|类型|必填|默认值|说明
:-|:-|:-|:-|:-
url|String|是||网络请求地址，如果项目中配置了apiPrefix并且setting中的apiPrefix为true，则添加配置的前缀
data|Object|否||要传的参数，会拼接在请求的url中
method|Object   |否||若cml.get()/cml.post()无法满足需求,如需使用DELETE/PUT时,可调用此方法
header|Object   |否||设置http请求的header
contentType|String|否|form|取值：form或json，决定body中data的格式，对应header中content-type为application/x-www-form-urlencoded或application/json
resDataType|String|否|json|设置response的数据类型, 为json时, 会尝试对返回值进行JSON.parse()
#### 举例
```cml.request({
     url: 'https://cml.com/api/user/1',
     data: {
       a: 1
     },
     method: 'PUT'
   }).then(res => {
     cml.showToast({
       message: JSON.stringify(res),
       duration: 2000
     })
   }, err => {
     cml.showToast({
       message: JSON.stringify(err),
       duration: 2000
     })
   })

```