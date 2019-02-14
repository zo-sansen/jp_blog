---
title: git 主branch地址被删除后更新报错问题解决
date: 2019-2-14
author: alanJiang
tags:
    - Git
categories:
    - Git
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: git 主branch地址被删除后更新报错问题解决
---
报错：
```
23:19	Update canceled

23:23	Can't Update
			No tracked branch configured for branch master or the branch doesn't exist.
			To make your branch track a remote branch call, for example,
			git branch --set-upstream-to origin/master master (show balloon)
```
解决方式：
>   git fetch

然后在执行
>   git push --set-upstream origin master

在更新就好了