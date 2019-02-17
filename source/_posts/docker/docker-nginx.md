---
title: docker-nginx
date: 2019-2-17
author: alanJiang
tags:
    - Docker
    - Nginx
categories:
    - Docker
thumbnail:  /img/docker/141209104153971.png
blogexcerpt: docker-nginx学习使用
---
查询
>docker search  nginx

拉取
>docker pull nginx

启动命令
>docker run -p 80:80 -v  -v  -d nginx
>docker run -p 80:80 --name mynginx -v /static:/static -v /etc/nginx/nginx.conf:/etc/nginx/nginx.conf -v $PWD/logs:/wwwlogs  -d nginx

nginx映射配置详解
- -v /static:/static：将主机中当前目录下的www挂载到容器的/www
- -v /etc/conf/nginx.conf:/etc/nginx/nginx.conf：将主机中当前目录下的nginx.conf挂载到容器的/etc/nginx/nginx.conf
- -v $PWD/logs:/wwwlogs：将主机中当前目录下的logs挂载到容器的/wwwlogs