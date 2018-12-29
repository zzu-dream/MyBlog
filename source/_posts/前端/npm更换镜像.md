---
title:  npm更换镜像
tags:  [npm更换镜像]
categories: [前端]
---

#### 由于不可说原因，npm install时，速度总是不尽如人意，解决办法是修改npm的数据源
`npm config set registry https://registry.npm.taobao.org`

	
#### 开发ReactNative项目，搭建环境时通过如下代码将npm设置成淘宝镜像

终端直接设置 

```
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
```

或者 编辑 ~/.npmrc 加入下面内容

```
registry = http://registry.cnpmjs.org
```

#### 修改后可以通过这个进行测试

```
	npm config get registry
	
	npm config get registry 
```	
	

[npm配置镜像、设置代理](https://segmentfault.com/a/1190000002589144)