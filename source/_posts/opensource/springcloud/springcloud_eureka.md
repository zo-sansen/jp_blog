---
title: SpringCloud服务注册中心
date: 2019-3-4
author: alanJiang
tags:
    - SpringCloud
categories:
    - SpringCloud
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: SpringCloud服务注册中心
---
版本使用
- spring-boot 2.0.2.RELEASE
- spring-cloud Finchley.RELEASE

# 单个服务注册中心

## pom.xml
```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.2.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

<properties>
    <java.version>1.8</java.version>
    <spring-cloud.version>Finchley.RELEASE</spring-cloud.version>
</properties>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

## 启动类
我们给启动类加上注解@EnableEurekaServer：

## application.yml
```
eureka:
  client:
    # 默认eureka服务注册中心会将自身作为客户端来尝试注册，所以我们需要禁用它的客户端注册行为
    register-with-eureka: false
    # 默认30秒会更新客户端注册上来的服务清单，启动时就不获取了，不然启动会有报错，虽然不影响
    fetch-registry: false
  server:
    # 关闭注册中心自我保护（默认是true，生产环境不建议关闭，去掉该配置项或改成true）
    enable-self-preservation: false
spring:
  application:
    name: eureka
server:
  port: 8761
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

# eureka客户端
## pom.xml
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
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
