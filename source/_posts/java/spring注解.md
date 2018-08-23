---
title:   spring注解
tags:  [spring]
categories:  [java]
date:  2018-06-11 16:17:22
---


## 背景
```
1、大量的XML让开发者厌恶,因此Spring提供了许多注解来完成各种功能。
2、大量的注解让开发者厌恶 ,因此Spring提供了组合注解来完成各种功能。
```

## Spring Boot 注解的意义以及作用

```
利用注解：隐式配置，例如：@Autowired、@Bean、@Component等，通过注解来简化xml文件。

利用Java文件：显示配置，比xml配置的优势是具备类型安全。

利用传统的xml配置文件。

```

注解(annotations)列表

@ResponseBody 

```
用该注解修饰的函数，会将结果直接填充到HTTP的响应体中，一般用于构建RESTful的api；

```
@Controller

```
用于定义控制器类，在spring 项目中由控制器负责将用户发来的URL请求转发到对应的服务接口（service层）。

```

@RestController

```
@ResponseBody和@Controller的合集

```
@RequestMapping

```
提供路由信息，负责URL到Controller中的具体函数的映射。

```

[更多注解详看](https://blog.csdn.net/m0_37995707/article/details/77447764)