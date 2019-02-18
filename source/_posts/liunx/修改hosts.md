---
title: 修改liunx hosts解析
date: 2019-2-13
author: alanJiang
tags:
    - HEXO
categories:
    - 个博搭建
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: 修改liunx hosts解析
---
修改/etc/hosts文件内容
添加一行，如github的
```
127.0.0.1	localhost
127.0.1.1	jp-System-Product-Name

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
0.0.0.0 account.jetbrains.com
13.229.188.59 github.com
```
