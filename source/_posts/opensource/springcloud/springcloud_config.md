---
title: SpringCloud配置中心
date: 2019-3-6
author: alanJiang
tags:
    - SpringCloud
categories:
    - SpringCloud
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: SpringCloud配置中心
---
版本使用
- spring-boot 2.0.2.RELEASE
- spring-cloud Finchley.RELEASE

# config server

## pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

## 启动类
@EnableConfigServer

## application.yml
### 使用git方式
```
server:
  port: 8666 #设置端口
spring:
  application:
    name: config-server #设置名称
  cloud:
    config:
      server:
        git:
          uri: https://gitee.com/dazhangyu/serverconfig.git #设置git仓库地址  对于ssh协议 不能用 呜呜呜
          username: 1433589043@qq.com
          password: 13317364876   #填写你自己密码
  security: 
      user: 
        name: root
        password: 123456
eureka:
    client:
       serviceUrl:
          defaultZone: http://192.168.3.5:8667/eureka/
```

### 本地环境
```
server:
  port: 8666 #设置端口
spring:
  profiles:
    active: native
  application:
    name: config-server #设置名称
  cloud:
    config:
      server:
        native:
          search-locations: classpath:/config
  security:
    user:
      name: root
      password: 123456
eureka:
  client:
    serviceUrl:
      defaultZone: http://192.168.3.5:8667/eureka/
```

如果客户端启动报错的话
加上
```
@Bean
public static PropertySourcesPlaceholderConfigurer placeholderConfigurer() {
    PropertySourcesPlaceholderConfigurer c = new PropertySourcesPlaceholderConfigurer();
    c.setIgnoreUnresolvablePlaceholders(true);
    return c;
}
```

# 高可用服务注册中心

只要eureka-server以不同端口启动多个实例即可，多个实例两两注册到对方。比如，
以8761端口启动一个Eureka Server端，注册到8762：
```
eureka:
  client:
    service-url:
      # 提供其他注册中心的地址，注册中心将自身以客户端注册的方式注册到其他注册中心去
      defaultZone: http://localhost:8761/eureka/
    register-with-eureka: false
    fetch-registry: false
  server:
    enable-self-preservation: false
spring:
  application:
    name: eureka
server:
  port: 8762
```

# config client
## pom.xml
```xml
<!--config 配置-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-client</artifactId>
</dependency>
```
## 启动类
@EnableDiscoveryClient

## application.yml
```
eureka:
  client:
    service-url:
      # 注册中心地址，如果注册中心是高可用，那么这里后面可以添加多个地址，逗号分开
      defaultZone: http://localhost:8761/eureka/
      #defaultZone: http://localhost:8761/eureka/,http://localhost:8762/eureka/
spring:
  application:
    name: client
```

# 模板
## pom.xml
```xml

```
## 启动类
## application.yml

---
{% raw %}
<style>
qq {
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
</style>
{% endraw %}
