---
title: docker下载安装
date: 2019-2-17
author: alanJiang
tags:
    - Docker
categories:
    - Docker
thumbnail:  /img/docker/141209104153971.png
blogexcerpt: docker下载安装
---
## ubuntu
安装
>apt-get install docker.io

创建软链接
>ln -sf /usr/bin/docker /usr/local/bin/docker

查看docker运行状态
>service docker status

启动docker服务
>service docker start

启动docker服务
>service docker start

关闭docker服务
>service docker stop

## centos
安装
>yum -y install docker-io

加入开机启动
>chkconfig docker on

启动docker服务
>service docker start 

