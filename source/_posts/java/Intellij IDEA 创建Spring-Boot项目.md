---
title:  Intellij IDEA 创建Spring-Boot项目
tags:  [Spring-Boot]
categories:  [java]
date:  2018-06-11 16:17:22
---


## 背景
### 1.1 SpringBoot简介

① 为所有Spring 开发提供一个更快更广泛的人门体验。

② 零配置。无冗余代码生成和XML 强制配置，遵循“约定大于配置” 。

③ 集成了大量常用的第三方库的配置， Spring Boot 应用为这些第三方库提供了几乎可以零配置的开箱即用的能力。

④）提供一系列大型项目常用的非功能性特征，如嵌入式服务器、安全性、度量、运行状况检查、外部化配置等。

### 1.2 Spring Boot 不是Spring 的替代者

        Spring 框架是通过IOC 机制来管理Bean 的。Spring Boot 依赖Spring 框架来管理对象的依赖。

        Spring Boot 并不是Spring 的精简版本，而是为使用Spring 做好各种产品级准备。

        简单的说，平常我们开发一个项目就好比组装一台电脑主机，需要我们自己购买各式各样的配件，最后把它们组装在一起。而Spring Boot 就好比是厂商帮我们组装好的品牌机电脑，各种常用的配件都帮我们封装好了，并且提供了许多的接口，只要我们想增加某个配件，或者修改某个配件的版本，只要跟他讲一下名称，都不需要我们自己去购买，他就会把配件送上门并且帮你装好，用springboot就是这么轻松！

### 1.3 Spring Boot 2 新特性

    目前Spring Boot 已经开发到了2.0.2版本 ，而我们之后的项目案例也是基于springboot2来开发的。

    Spring Boot 2 基于最新的Java 8 和Spring Framework 5 ，这意味着Spring Boot 2 拥有构建现代应用的能力。

    ( 1 ）基于Java 8 的反射增强， Spring Framework 5.0 中的方法参数可以更加高效地进行访问。  
    ( 2 ）接口提供基于Java 8 的默认方法构建的选择性声明。  
    ( 3 ）支持候选组件索引作为类路径扫描的替代方案。  
    ( 4 ）当然，最为重要的是， 此次Spring Framework 5.0 推出了新的响应式堆钱WEB 框架。  

相应地， Spring Boot 2 会集成最新的技术枝，包括Spring Data 、Spring Security 、Spring Integration 、Spring  AMQP, Spring Session 、Spring Batch 等都做了更新，其他的第三方依赖也会尝试使用最新的版本。

毫无疑问，Spring Boot  是一种趋势，同时我们在使用spring boot 的同时也在使用着其它新的技术框架。


[Intellij IDEA 创建Spring-Boot项目](https://blog.csdn.net/u014296316/article/details/79382186)  
[使用Intellij IDEA创建SpringBoot项目](https://blog.csdn.net/zyhlwzy/article/details/78730587)  
[基于SpringBoot开发一套完整的项目](https://blog.csdn.net/xwd718/article/details/80640357)