---
title: HexoCommand
tags:
    - HEXO
    - HEXO_GitHub个博
categories:
    - 个博搭建
author: alanJiang
thumbnail: /img/thumbnail/hexocommand.jfif
blogexcerpt: 简介hexo常用写作命令。
---

# HEXO常用写作命令
## 1.创建markdown文件
>   语法：hexo new [layout] <title>
>   参解：
>   - hexo:hexo命令
>   - new:创建
>   - layout:布局,Hexo 有三种默认布局：post、page 和 draft，默认post布局

布局名称|路径
:---|:--
post|source/_posts
page|source
draft|source/_drafts

## 2.模版（Scaffold）
在新建文章时，Hexo 会根据 scaffolds 文件夹内相对应的文件来建立文件
例：
> $ hexo new photo "MyHexoWord"

在执行这行指令时，Hexo 会尝试在 scaffolds 文件夹中寻找 photo.md，并根据其内容建立文章，以下是您可以在模版中使用的变量

变量|描述
:---|:--
layout|布局
title|标题
date|文件建立日期
