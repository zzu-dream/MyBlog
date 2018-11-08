
---
title: React项目创建 与 redux的使用
tags: React
categories: React
date:  2018-10-30 14:17:22
---

### 初始化一个react项目
* `create-react-app`是一个通过`npm`发布的安装包，在确认`Node.js`和`npm`安装好之后，输入下面命令创建。  
	`npm install -g create-react-app`
* 安装结束后，使用下面命令创建应用目录。  
	`create-react-app test-app ` 
* 打开目录  
	`cd test-app`
* 运行项目  
	`npm start` 
	
### 基于create-react-app的再配置

[使用react-app-rewired来进行react的再配置](https://www.cnblogs.com/xiaohuochai/p/8491055.html)

### 如何优雅地在React项目中使用Redux

[使用Redux](https://www.cnblogs.com/sampapa/p/8134086.html)

``` js
npm install --save redux react-redux redux-thunk
npm install --save-dev redux-logger
```

**相关库说明**  

* **React** UI框架
* **Redux** 状态管理工具，与React没有任何关系，其他UI框架也可以使用Redux

* **react-redux** React插件，作用：方便在React项目中使用Redux

* **react-thunk** 中间件，作用：支持异步action

**Redux三大原则**  

* 单一数据源  
整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中
* State 是只读的
唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象
* 使用纯函数来执行修改
为了描述 action 如何改变 state tree ，你需要编写 reducers

### 外部优秀网站
[React 入门 ruanyifeng](http://www.ruanyifeng.com/blog/2015/03/react.html)  
[React入门篇](https://segmentfault.com/a/1190000012921279)  
[React 中文索引](http://nav.react-china.org/)  
[react-collection](https://github.com/LeuisKen/react-collection)  
[Ant Design of React](https://ant.design/docs/react/introduce-cn)  
[Drag and Drop for React](http://react-dnd.github.io/react-dnd/)  
[Redux 入门教程](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)