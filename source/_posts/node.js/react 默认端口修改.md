---
title:  react 默认端口修改
tags:  [react 默认端口修改]
categories: [前端]
---

#### 修改react port的方法

执行npm start便可启动项目，所以不管是react怎么升级，找修改端口的位置，我们首先都应该想到看一下package.json里面的配置信息。如果你是先前创建的项目，端口的修改是在scripts文件夹的start.js文件里。但是现在创建的项目里没有了scripts文件夹了，但看package.json会发现它放到了依赖里面，在node_modules文件夹里的可以看到react-scripts文件夹，在start.js里可以找到修改端口的代码。

#### 依赖的模块放在哪
* dependencies: 指定项目运行所依赖的模块，即：开发版和发布版都需要的依赖。

* devDependencies:指定项目开发所需要的模块，即：开发版需要但发布版不需要，例如关于测试的、文档类的。


npm install <package_name> --save 表示将这个包名及对应的版本添加到 package.json的 dependencies
npm install <package_name> --save-dev 表示将这个包名及对应的版本添加到 package.json的 devDependencies


	

[react 默认端口修改](https://blog.csdn.net/weixin_37242696/article/details/80654508)