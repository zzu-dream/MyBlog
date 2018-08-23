---
title:   java-spring
tags:  [spring]
categories:  [java]
date:  2018-06-11 16:17:22
---

## spring框架

```
Spring是一个开放源代码的设计层面框架，他解决的是业务逻辑层和其他各层的松耦合问题，
因此它将面向接口的编程思想贯穿整个系统应用。
Spring是于2003 年兴起的一个轻量级的Java 开发框架，由Rod Johnson创建。
简单来说，Spring是一个分层的JavaSE/EE full-stack(一站式) 轻量级开源框架。
```

## 下载和安装Spring请按如下步骤进行。
（1）登录站点，下载Spring的最新稳定版本。最新版本为spring-framework-5.0.建议下载spring-framework-spring-framework-4.0.0.M2-dist这个压缩包不仅包含Spring的开发包，而且包含Spring编译和运行所依赖的第三方类库。
解压缩下载到的压缩包，解压缩后的文件夹应用如下几个文件夹。  
dist：该文件夹下放Spring的jar包，通常只需要Spring.jar文件即可。该文件夹下还有一些类似spring－Xxx.jar的压缩包， 这些压缩包是spring.jar压缩包的子模块压缩包。除非确定整个J2EE应用只需要使用Spring的某一方面时，才考虑使用这种分模块压缩包。通常建议使用Spring.jar  
docs：该文件夹下包含spring的相关文档、开发指南及API参考文档。  
lib：该文件夹下包含spring编译和运行所依赖的第三方类库，该路径下的类库并不是  spring必需的，但如果需要使用第三方类库的支持，这里的类库就是必需要的。  
samples：该文件夹下包含Spring的几个简单例子，可作为Spring入门学习的案例。  
src：该文件夹下包含Spring的全部源文件，如果开发过程中有地方无法把握，可以参考该源文件，了解底层实现。  
spring  
spring
test：该文件夹下包含Spring的测试示例。
tiger：该路径下存放关于JDK的相关内容
解压缩后的文件夹下，还包含一些关于Spring的License和项目相关文件    
（2）将spring.jar复制到项目的CLASSPATH路径下，对于Web应用，将spring.jar文件复制到WEB-INF/lib路径下，该应用即可以利用Spring框架了。  
（3）通常Spring的框架还依赖于其他一些jar文件，因此还须将lib下对应的包复制到WEB-INF/lib路径下，具体要复制哪些jar文件，取决于应用所需要使用的项目。通常需要复制cglib，dom4j，jakarta-commons，log4j等文件夹下的jar文件。  
（4）为了编译java文件，可以找到Spring的基础类，将Spring.jar文件的路径添加到环境变量CLASSPATH中。当然，也可以使用ANT工具，但无须添加环境变量。如果使用Eclipse或者NetBeans等IDE时，也不需要设置环境变量。  
## Spring MVC  
传统的web架构的view 表现层使用struts作为表现层。但是如果试用下spring自带的MVC，会发现spring 在一般场合完全可以取代struts。从某些角度来说，spring的mvc设计的更加合理，有兴趣的话不妨尝试下单个的spring的MVC。

[w3Cschool-spring学习](https://www.w3cschool.cn/wkspring/)

## Spring Boot 是什么？

```
Spring Boot 的目的是提供一组工具，以便快速构建容易配置的 Spring 应用程序。

```

