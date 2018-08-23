---
title:  weex 工作原理
tags:  [weex 工作原理]
categories:  [weex]
date:  2018-06-11 16:17:22
---


## weex 工作原理

```
transformer 会把 template, style, script 都转换成一段段 json 或者 js，
这样客户端只接收并运行js，不必同时解析html/css这些语法，并且这些js还会继续进行
数据监听和绑定，然后生成最终的virtual dom 再发送给 native端进行渲染。
```
![](https://raw.githubusercontent.com/yongbolv/images/master/weexframework.png)

## weex 主要就是做了三件事
1. 在服务端用 Transformer 工具把 Vue 代码转换成 Js Bundle。
2. 在客户端运行Js Framework 的 JavaScript 引擎，解释执行Js Bundle生成Virtual DOM。
3. 在客户端设计一套 JS Bridge，能使IOS端（或者Android端）的Object-C语言（或Java语言）与Javascript语言相互调用，把Virtual Dom转换为DOM，渲染到页面。H5端直接和Js Framework 通讯，不需要Js Bridge。
如下为Virtual DOM 渲染为Dom的过程：
![](https://raw.githubusercontent.com/yongbolv/images/master/virtualdom.png)

## 相关概念：

```
ECMAScript：定义了JavaScript语言的标准
JavaScriptCore：应用在在wekit内核内的js引擎，浏览器有Safari。
V8: 应用在chromium内的js引擎，浏览器有Chrome。
JS引擎的作用都是解释和执行JavaScript代码。

```
有关JavaScript引擎解析的内容请查看  [JavaScriptCore解析](http://www.uml.org.cn/codeNorms/201306063.asp)

有关JavaScriptCore和V8的内容请查看：[JavaScript引擎](http://blog.csdn.net/milado_nju/article/details/22101681)


## 怎么开始搭建个weex项目

相对比较简单看官方吧。
weex相关工具

```
node.js
weex-toolkit
Weex Playground App
```

## 相关论坛

[weex 文章](https://github.com/weexteam/article/issues)
[weex 调试](https://github.com/weexteam/article/issues/50)
[weex 文档：](http://alibaba.github.io/weex/doc/)
[weex中使用数据流工具Vuex实践](http://www.kmhaoshuai.com/#!/articles/use-vuex-in-weex)
[weex交流室](http://lvyongbo.net/2016/09/27/weex技术工作原理/%C2%A0https://gitter.im/weexteam/cn?utm_source=share-link&utm_medium=link&utm_campaign=share-link)





