---
title: MarkDown
tags:
  - MarkDown
  - HEXO_GitHub个博
categories:
  - 个博搭建
author: alanJiang
thumbnail: /img/thumbnail/markdown.jpg
blogexcerpt:  markdown常见用法学习与使用,并整理相关资源信息。
---


#***markdown常见用法***
>不管你是开发，还是产品，还是测试，还是普通软件使用的运营人员，总之，学会了markdown会对你的工作，生活有莫大的帮助。

###***有哪些使用markdown的产品呢？***
- GitHub
- 简书
- CSDN
- Stack Overflow
- Apollo
- 等等

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
>       `create database hero;`

`create database hero;`

### 2.代码块
语法：代码之间分别用三个反引号包起来，且两边的反引号单独占一行

>       \`\`\`
>           function fun(){
>           echo "这是一句非常牛逼的代码";
>           }
>           fun();
>        \`\`\`

```
    function fun(){
         echo "这是一句非常牛逼的代码";
    }
    fun();
```

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

事例：\!\[markdown创始人](/resource/the-hound_big_2_.gif)
![markdown创始人](https://raw.githubusercontent.com/alanjiang1129/markdown/master/resource/the-hound_big_2_.gif)

### 图片大小(暂时不知道为什么不行)

语法
> \!\[](...=300-300-r)

![markdown创始人](https://raw.githubusercontent.com/alanjiang1129/markdown/master/resource/the-hound_big_2_.gif =300-300-r)

### html标签方式
>       <p align="left">
>           <img src="https://raw.githubusercontent.com/alanjiang1129/markdown/master/resource/the-hound_big_2_.gif" alt="Sample"  width="250" height="140">
>           <p align="left">
>               <em>html图片示例</em>
>           </p>
>       </p>

<p align="left">
    <img src="https://raw.githubusercontent.com/alanjiang1129/markdown/master/resource/the-hound_big_2_.gif" alt="Sample"  width="250" height="140">
    <p align="left">
        <em>html图片示例</em>
    </p>
</p>
## 九.超链接
语法
>   [超链接名](超链接地址 "超链接title")
>   - title可以不加

>   \[百度](www.baidu.com)
>   \[百度](www.baidu.com)

>   [百度](https://www.baidu.com)
>   [必应](https://cn.bing.com/)
    [谷歌](https://www.google.com/)
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
刘备 | 关羽 | 张
## 十一.markdown绘制流程图
放弃这个东西:joy:，不好用还复杂，觉得还是xmind直接画比较简单粗暴。



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

## git:Emoji表情(github特有的特性)
:sleeping:
:anguished:
:raised_hand:
> [github常用表情代码地址](https://www.webfx.com/tools/emoji-cheat-sheet/)

## IDE:编辑器
- markdown属于轻量级标记语言
>   1. 很多系统文本编辑器都可以编辑，windows的记事本，常用的notepad++,liunx的vim,vi都可以
>   2. 笔者是java开发人员，使用的vscode，idea都有对应插件
>   3. google浏览器插件：StackEdit Markdown Extension(该官网不一定有下载)[官网](https://stackedit.io/)[在线模式](https://stackedit.io/app#)/Markdown-here[官网](https://markdown-here.com/index.html)等，扩展应用商城搜索”Markdown“有很多,(无法访问google搜索的可以去相关插件网站下载，离线安装google插件)

## other
- 反斜杠\：转义符

