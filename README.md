---
title: 帅比鹏
date: 2017-7-7
author:
tags:
    - 测试
categories:
    - hexo
thumbnail:
blogexcerpt:
---

# markdown入门
        
## 一.标题
>      #一级标题
>      ## 二级标题
>      ### 三级标题
>      #### 四级标题
>      ##### 五级标题
>      ###### 六级标题
## 二.段落
> table键
## 三.区块引用
>       >
>       或者
>       >>
>       或者更多
## 四.代码区块
### 1.单行代码
语法：代码之间分别用一个反引号（``）包起来

`create database hero;`

### 2.代码块
语法：代码之间分别用三个反引号包起来，且两边的反引号单独占一行

(```)
    function fun(){
         echo "这是一句非常牛逼的代码";
    }
    fun();
(```)

### 3.直接tab
    void main()
    {
        printf("Hello Markdown Use AlanJiang");
    }
## 五.列表
###1.无序列表
>使用星号（*），加号（+），减号（-）作列表标记

>       - a
>       + b
>       * c

> - a
> + b
> * c
###2.有序列表
>使用数字加点作列表标记

>       1. a
>       2. b
>       3. c

> 1. a
> 2. b
> 3. c
###3.嵌套
>嵌套列表

>       1. a
>           1. a1
>           2. a1

> 1. a
>   1. a1
>   2. a1

>嵌套列表无序

>       - a
>           - a1
>           - a2

>  - a
>     - a1
>     - a2
## 六.字体样式
1. 加粗
> \**word\** **word**   
2. 斜体
> \*word\* *word*  
3. 斜体加粗
> \***word\*** ***word***   
4. 删除线
> \~\~word\~\~  ~word~~ 
## 七.分割线
> 三个或者三个以上的 - 或者 * 都可以。
## 八.图片
语法
>   \!\[alt\](src "title")
>   - alt图片下面文字
>   - src图片地址
>   - title鼠标移到图片上时显示的内容

事例：\!\[markdown创始人](https://github.com/younghz/Markdown/raw/master/resource/Aaron_Swartz.jpg)
![markdown创始人](https://cdn.dribbble.com/users/244516/screenshots/2766513/the-hound_big_2_.gif)
## 九.超链接
语法
>   [超链接名](超链接地址 "超链接title")
>   - title可以不加

>   \[百度](www.baidu.com)
>   \[百度](www.baidu.com)

>   [百度](www.baidu.com)

>   [百度](www.baidu.com)
## 十.表格

>       表头|表头|表头
>       :---|:--:|---:
>       内容|内容|内容
>       内容|内容|内容
> - "\-"有一个就可以了
> - "\:"对其方式

java | html | js
:-   | :-:  | -:
小明1234 | 小黄1324 | 小亮123
刘备 | 关羽 | 张飞

## git:复选框(github特有的特性)
>       - [ ] 不勾选
>       - [x] 勾选
- [ ] 不勾选
- [x] 勾选
- [x] C
- [x] C++
- [x] Java
- [x] Qt
- [x] Android
- [ ] C#
- [ ] .NET
