---
title: nginx入门
date: 2019-2-16
author: alanJiang
tags:
    - Nginx
categories:
    - Nginx
thumbnail:  \img\nginx\bg2018022701.png
blogexcerpt: nginx 学习使用
---
NGINX是一个免费的，开源的，高性能的HTTP服务器和反向代理，以及IMAP / POP3代理服务器。NGINX以其高性能，稳定性，丰富的功能集，简单的配置和低资源消耗而闻名。

# 安装
## linux安装
[nginx下载](http://nginx.org/download/nginx-1.6.2.tar.gz)

## nginx常用命令
### 启动服务
>/usr/local/nginx/sbin/nginx
### 停止服务
>/usr/local/nginx/sbin/nginx -s stop
### 检验nginx配置有没有用
>/usr/local/nginx/sbin/nginx -t
### 平滑重启nginx
>/usr/nginx/sbin/nginx -s reload
### 正常关闭服务
>/usr/nginx/sbin/nginx -s quit
### 重新打开日志文件
>/usr/nginx/sbin/nginx -s reopen
### 信号
>/usr/nginx/sbin/nginx -s signal

## 语法
一行语句已";"结尾，一个程序块以“{}”包括起来，大括号中有其他大括号指令，可以“，”隔

## 配置
###  编译时配置
