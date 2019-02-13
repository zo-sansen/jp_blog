---
title: 微服务架构盛行的时代，你需要了解点 Spring Boot
tags:
    - SpringBoot
categories:
    - SpringBoot
author: alanJiang
thumbnail: /img/thumbnail/springboot.jfif
blogexcerpt:  微服务架构盛行的时代，你需要了解点 Spring Boot，帮助java程序员快速开发。
---
随着互联网的高速发展，庞大的用户群体和快速的需求变化已经成为了传统架构的痛点。在这种情况下，如何从系统架构的角度出发，构建出灵活、易扩展的系统来快速响应需求的变化，同时，随着用户量的增加，如何保证系统的稳定性、高可用性、可伸缩性等等，成为了系统架构面临的挑战。

为了解决这些问题，微服务架构应运而生，它的本质在于分布式、去中心化。微服务架构是一种架构模式或者说一种架构风格，它提倡将传统的一站式应用（左下图）根据业务拆分成一个个服务（右下图），彻底去掉耦合，每个服务提供单个业务功能，一个服务只做一件事，运行在其独立的进程中。

![](https://diycode.b0.upaiyun.com/photo/2019/8fb83bbe7fb11df3bce0c919238a879e.jpg)

每个服务之间互相协调、互相配合，为用户提供最终的价值。服务之间采用轻量级的通信机制（通常是基于 http 的 RESTful API）。

每个服务都围绕着具体业务进行构建，并且能够被独立地部署到生产环境、类生产环境等。不同的服务也可以使用不同的数据库和数据存储。

![](https://diycode.b0.upaiyun.com/photo/2019/141fa23a877d00474aee3ed9ead8552e.jpg)

另外，应尽量避免统一的、集中式的服务管理机制，对具体的一个服务而言，应根据业务上下文，选择合适的语言、工具对其进行构建，可以有一个非常轻量级的集中式管理来协调这些服务，可以使用不同的语言来开发这些服务。

Spring Boot 诞生时，微服务概念正处于酝酿阶段，Spring Boot 的研发融合了微服务架构的理念，是 Java 领域微服务架构最优落地的技术，给微服务架构提供了技术支撑。Spring Boot 有哪些优势呢？

![](https://diycode.b0.upaiyun.com/photo/2019/02b185884dc4fdda3a268dabf8f3747e.jpg)

- 良好的基因：Spring Boot 是伴随着 Spring 4.0 诞生的，继承了 Spring 框架的优秀基因。
- 简化编码：传统的 Spring web 项目需要引入一堆相关的依赖，而在 Spring Boot 中，我们只需要引入一个  starter-web 依赖即可快速创建 web 应用。
- 简化配置：传统的 Spring 项目一度被人认为是“配置地狱”，而 Spring Boot 更多的是采用 Java Config 的方式，简化了配置的繁琐。
- 简化部署：Spring Boot 项目不需要在服务器上去部署 tomcat，因为 Spring Boot 内嵌了 tomcat，我们只需要将项目打成 jar 包，通过命令一键式启动。
- 简化监控：可以引入 spring-boot-start-actuator 依赖，直接使用 REST 方式来获取进程的运行期性能参数，从而达到监控的目的，还可以配合 Spring Cloud 一起使用。

微服务是未来发展的趋势，使用 Spring Boot 开发项目，会颠覆传统的开发模式，大大提升开发效率，可以说如果你使用 Spring Boot 开发过项目，你就不愿意再回到原来的开发方式了。

看看 Spring 官方对 Spring Boot 的定位：Build Anything，Build 任何东西。

![](https://diycode.b0.upaiyun.com/photo/2019/23202265f7a330bfbb378194afb3e31a.jpg)

Spring Boot 旨在尽可能快地启动和运行，并且只需最少的 Spring 前期配置。 同时我们也来看一下官方对后面两个的定位：
- SpringCloud：Coordinate Anything，协调任何事情；
- SpringCloud Data Flow：Connect everything，连接任何东西。

仔细品味一下，Spring 官网对 Spring Boot、SpringCloud 和 SpringCloud Data Flow 三者定位的措辞非常有味道，同时也可以看出，官方对这三个技术非常重视，我们还有什么理由不去学习呢？