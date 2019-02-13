---
title: Docker部署GitLab
author: alanJiang
tags:
  - Docker
  - GitLab
categories:
  - Docker
thumbnail: /img/thumbnail/GitLab-CI-logo.jpg
blogexcerpt: Docker部署GitLab
---


# 前言
Git 是目前最流行的版本控制系统，在它的基础之上， GitHub 和 GitLab 成为当前最流行的代码托管平台，它们均提供的代码评审、项目管理、持续集成等功能，越来越多的互联网企业都迁移到 Git。

# 部署
为了安装方便，这里我们使用 Docker 安装 GitLab 中文版，通常会将 GitLab 的配置 (config) 、 日志 (logs) 、数据 (data) 放到容器之外， 便于日后升级：

        docker run \
            --detach \
            --publish 8443:443 \
            --publish 8000:80 \
            --name gitlab \
            --restart unless-stopped \
            --volume /srv/gitlab/config:/etc/gitlab:Z \
            --volume /srv/gitlab/logs:/var/log/gitlab:Z \
            --volume /srv/gitlab/data:/var/opt/gitlab:Z \
            beginor/gitlab-ce:11.3.0-ce.0

修改/srv/gitlab/config/gitlab.rb 文件：
>        # 配置端口
>        unicorn['port'] = 8084
>        # 这个地址一定要配置、否则项目的Git地址不对
>        external_url "http://192.168.1.180"
>        # 配置邮件
>        gitlab_rails['smtp_enable'] = true
>        gitlab_rails['smtp_address'] = "smtp.163.com"
>        gitlab_rails['smtp_port'] = 25
>        gitlab_rails['smtp_user_name'] = "17762018584@163.com"
>        gitlab_rails['smtp_password'] = "111111"
>        gitlab_rails['smtp_domain'] = "163.com"
>        gitlab_rails['smtp_authentication'] = "login"
>        gitlab_rails['smtp_enable_starttls_auto'] = true
>        gitlab_rails['smtp_tls'] = false
>        gitlab_rails['gitlab_email_from'] = "17762018584@163.com"
>        user["git_user_email"] = "17762018584@163.com"

配置密钥
输入命令，一直回车即可。
>       $ ssh-keygen -t rsa -C '345849402@qq.com'
>       Generating public/private rsa key pair.
 >       Enter file in which to save the key (/c/Users/zzp/.ssh/id_rsa):
 >       Created directory '/c/Users/zzp/.ssh'.
 >       Enter passphrase (empty for no passphrase):
 >       Enter same passphrase again:
 >       Your identification has been saved in /c/Users/zzp/.ssh/id_rsa.
 >       Your pub*lic key has been saved in /c/Users/zzp/.ssh/id_rsa.pub.
 >       The key fingerprint is:
 >       SHA256:OoPvUUq6XgrqdBGXmY9nZIJAR6jQxF702hdLEPVTKkk 345849402@qq.com
 >       The key's randomart image is:
 >       +---[RSA 2048]----+
 >       |.*++. ooE   .    |
 >       |..= o.+o o o     |
 >       |o. + *.o= +      |
 >       |. . oo*. + .     |
 >       |   ...o+S        |
 >       |    .+o=         |
 >       | ...o B          |
 >       |.... = +         |
 >       |o. .+.o          |
 >       +----[SHA256]-----+
 
 Gitlab命令
 
 >      # 重新应用gitlab的配置
 >      gitlab-ctl reconfigure
 
 >      # 重启gitlab服务
 >      gitlab-ctl restart
 
 >      # 查看gitlab运行状态
 >      gitlab-ctl status
 
 >      #停止gitlab服务
 >      gitlab-ctl stop
 
 >      # 查看gitlab运行日志
 >      gitlab-ctl tail
 
 >      # 停止相关数据连接服务
 >      gitlab-ctl stop unicorn
 >      gitlab-ctl stop sideki
 
  界面效果
  ![1](/img/thumbnail/gitoauth3.png)