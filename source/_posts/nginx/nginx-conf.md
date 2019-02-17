---
title: nginx-conf配置
date: 2019-2-17
author: alanJiang
tags:
    - Nginx
categories:
    - Nginx
thumbnail:  \img\nginx\bg2018022701.png
blogexcerpt: nginx-conf常用配置信息
---
# 简介
Nginx配置文件主要分成四部分
1. main：全局配置
2. server：主机配置
3. upstream：上游服务器设置，主要为反向代理、负载均衡相关配置
4. location：URL匹配特定位置后的设置

<p class='pp'>server继承main，location继承server；upstream既不会继承指令也不会被继承。它有自己的特殊指令，不需要在其他地方的应用</p>

# 配置
### 1.main全局配置
#### 直接写在根
- <tt>woker_processes 2</tt>：设置cpu使用使用数量
- <tt>worker_cpu_affinity</tt>：在高并发情况下，通过设置cpu粘性来降低由于多CPU核切换造成的寄存器等现场重建带来的性能损耗
  如<aaa>worker_cpu_affinity 0001 0010 0100 1000</aaa>(四核)
- <tt>worker_rlimit_nofile 10240</tt>：写在main部分。默认是没有设置，可以限制为操作系统最大的限制65535。

#### events模块
- <tt>worker_connections 2048</tt>：每一个worker进程能并发处理（发起）的最大连接数（包含与客户端或后端被代理服务器间等所有连接数）
    nginx作为反向代理服务器计算公式 <aaa>最大连接数 = worker_processes * worker_connections/4</aaa> 所以这里客户端最大连接数是1024,设置不能超过<aaa>worker_rlimit_nofile</aaa>
    当nginx作为http服务器时，计算公式里面是除以2。
- <tt>use epoll</tt>：
    Linux操作系统下，nginx默认使用epoll事件模型，得益于此，nginx在Linux操作系统下效率相当高。
    OpenBSD或FreeBSD操作系统上采用类似于epoll的高效事件模型kqueue。
    在操作系统不支持这些高效模型时才使用select。

### 2.http服务器模块
- <tt>sendfile on</tt>：开启高效文件传输模式，sendfile指令指定nginx是否调用sendfile函数来输出文件，减少用户空间到内核空间的上下文切换。对于普通应用设为 on，如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络I/O处理速度，降低系统的负载。
- <tt>keepalive_timeout 65</tt>：长连接超时时间，单位是秒，这个参数很敏感，涉及浏览器的种类、后端服务器的超时设置、操作系统的设置，可以另外起一片文章了。长连接请求大量小文件的时候，可以减少重建连接的开销，但假如有大文件上传，65s内没上传完成会导致失败。如果设置时间过长，用户又多，长时间保持连接会占用大量资源。
- <tt>send_timeout</tt>：用于指定响应客户端的超时时间。这个超时仅限于两个连接活动之间的时间，如果超过这个时间，客户端没有任何活动，Nginx将会关闭连接。
- <tt>client_max_body_size 10m</tt>：允许客户端请求的最大单文件字节数。如果有上传较大文件，请设置它的限制值
- <tt>client_body_buffer_size 128k</tt>：缓冲区代理缓冲用户端请求的最大字节数
- <tt>default_type</tt>：default_type  application/octet-stream;
- <tt>test</tt>：
#### 模块http_proxy（这个模块实现的是nginx作为反向代理服务器的功能，包括缓存功能）【设置直接写在http大括号根目录】：
- <tt>proxy_connect_timeout 60</tt>：nginx跟后端服务器连接超时时间(代理连接超时)
- <tt>proxy_read_timeout 60</tt>：连接成功后，与后端服务器两个成功的响应操作之间超时时间(代理接收超时)
- <tt>proxy_buffer_size 4k</tt>：设置代理服务器（nginx）从后端realserver读取并保存用户头信息的缓冲区大小，默认与proxy_buffers大小相同，其实可以将这个指令值设的小一点
- <tt>proxy_buffers 4 32k</tt>：proxy_buffers缓冲区，nginx针对单个连接缓存来自后端realserver的响应，网页平均在32k以下的话，这样设置
- <tt>proxy_busy_buffers_size 64k</tt>：高负荷下缓冲大小（proxy_buffers*2）
- <tt>proxy_max_temp_file_size</tt>：当proxy_buffers放不下后端服务器的响应内容时，会将一部分保存到硬盘的临时文件中，这个值用来设置最大临时文件大小，默认1024M，它与proxy_cache没有关系。大于这个值，将从upstream服务器传回。设置为0禁用。
- <tt>proxy_temp_file_write_size 64k</tt>：当缓存被代理的服务器响应到临时文件时，这个选项限制每次写临时文件的大小。<aaa>proxy_temp_path</aaa>：（可以在编译的时候）指定写到哪那个目录。
#### 模块http_gzip
- <tt>gzip on</tt>：开启gzip压缩输出，减少网络传输。
- <tt>gzip_min_length 1k</tt>：设置允许压缩的页面最小字节数，页面字节数从header头得content-length中进行获取。默认值是20。建议设置成大于1k的字节数，小于1k可能会越压越大。
- <tt>gzip_buffers 4 16k</tt>：设置系统获取几个单位的缓存用于存储gzip的压缩结果数据流。4 16k代表以16k为单位，安装原始数据大小以16k为单位的4倍申请内存。
- <tt>gzip_http_version 1.0</tt>： 用于识别 http 协议的版本，早期的浏览器不支持 Gzip 压缩，用户就会看到乱码，所以为了支持前期版本加上了这个选项，如果你用了 Nginx 的反向代理并期望也启用 Gzip 压缩的话，由于末端通信是 http/1.0，故请设置为 1.0。
- <tt>gzip_comp_level 6</tt>：gzip压缩比，1压缩比最小处理速度最快，9压缩比最大但处理速度最慢(传输快但比较消耗cpu)
- <tt>gzip_types</tt>：匹配mime类型进行压缩，无论是否指定,”text/html”类型总是会被压缩的。举例：<aaa>gzip_types text/html text/plain text/css</aaa>
- <tt>gzip_vary on</tt>：和http头有关系，会在响应头加个 Vary: Accept-Encoding ，可以让前端的缓存服务器缓存经过gzip压缩的页面，例如，用Squid缓存经过Nginx压缩的数据。

#### server虚拟主机
http服务上支持若干虚拟主机，每个server通过监听地址或端口来区分。
- <tt>listen</tt>：监听端口，默认80，小于1024的要以root启动。可以为listen *:80、listen 127.0.0.1:80等形式。
- <tt>server_name</tt>：服务器名，如localhost、www.example.com，可以通过正则匹配。
##### 1.模块http_stream（负载均衡）
这个模块通过一个简单的调度算法来实现客户端IP到后端服务器的负载均衡，upstream后接负载均衡器的名字，后端realserver以 host:port options; 方式组织在 {} 中。如果后端被代理的只有一台，也可以直接写在 proxy_pass 。
例如：
upstream分配策略全解：
- weight（权重）：指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。如下所示，10.0.0.88的访问比率要比10.0.0.77的访问比率高一倍。
```upstream linuxidc{ 
       server 10.0.0.77 weight=5; 
       server 10.0.0.88 weight=10; 
 }
 ```
- ip_hash（访问ip）：每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session的问题。
```
upstream favresin{ 
      ip_hash; 
      server 10.0.0.10:8080; 
      server 10.0.0.11:8080; 
}
```
- fair（第三方）：按后端服务器的响应时间来分配请求，响应时间短的优先分配。与weight分配策略类似。
```
upstream favresin{      
      server 10.0.0.10:8080; 
      server 10.0.0.11:8080; 
      fair; 
}
```
- url_hash（第三方）：按访问url的hash结果来分配请求，使每个url定向到同一个后端服务器，后端服务器为缓存时比较有效。
    注意：在upstream中加入hash语句，server语句中不能写入weight等其他的参数，hash_method是使用的hash算法。
 ```
 upstream resinserver{ 
      server 10.0.0.10:7777; 
      server 10.0.0.11:8888; 
      hash $request_uri; 
      hash_method crc32; 
}
```
<t>其他设置状态项</t>
>   - down：表示单前的server暂时不参与负载.
>   - weight：表示单前的server暂时不参与负载.
>   - max_fails ：允许请求失败的次数默认为1.当超过最大次数时，返回proxy_next_upstream 模块定义的错误.
>   - fail_timeout  ：max_fails次失败后，暂停的时间。
>   - backup  ：其它所有的非backup机器down或者忙的时候，请求backup机器。所以这台机器压力会最轻。

```
将server节点下的location节点中的proxy_pass配置为：http:// + upstream名称，即“
http://backend”.

location / { 
            root  html; 
            index  index.html index.htm; 
            proxy_pass http://backend; 
}
```


##### 2.location（http服务中，某些特定的URL对应的一系列配置项。）
- <t>root /var/www/html</t>：定义服务器的默认网站根目录位置。如果locationURL匹配的是子目录或文件，root没什么作用，
    一般放在server指令里面或/下。server下的和location下的不会重复,常用于静态文件。
- <tt>index index.jsp index.html index.htm</tt>：定义路径下默认访问的文件名，一般跟着root放
- <tt>proxy_pass http:/backend</tt>：请求转向backend定义的服务器列表，即反向代理，对应upstream负载均衡器。也可以<aaa>proxy_pass  http://ip:port</aaa>
- <tt>proxy_redirect off;</tt>
<tt>proxy_set_header Host $host;</tt>
<tt>proxy_set_header X-Real-IP $remote_addr;</tt>
<tt>proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;</tt>
    这四个暂且这样设，如果深究的话，每一个都涉及到很复杂的内容，也将通过另一篇文章来解读。


- <tt>test</tt>：
- <tt>test</tt>：

---
[推荐地址1](https://segmentfault.com/a/1190000002797601#articleHeader5)
[推荐地址2](https://www.jianshu.com/p/a7c86efe1987)
[推荐地址3](https://www.zybuluo.com/phper/note/89391)
{% raw %}
<style>
.pp{
    color: red;
    font-style: oblique;
    font-weight: bold;
    margin: 10px 10px;
}
aaa {
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
 
 tt {
      padding: 2px 4px;
      font-size: 14px;
     color: #2087b9;
     font-weight: bold;
     background-color: #51cc8730;
      border-radius: 4px;
  }
</style>
{% endraw %}
