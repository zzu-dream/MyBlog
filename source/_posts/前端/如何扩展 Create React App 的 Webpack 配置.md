
---
title: 如何扩展 Create React App 的 Webpack 配置
tags: React webpack配置
categories: React
date:  2018-10-30 14:17:22
---
### 配置方式
其实我们可以通过以下几种方式来修改 webpack 的配置：

* 项目 eject
* 替换 react-scripts 包
* 使用 react-app-rewired
* scripts 包 + override 组合


[如何扩展 Create React App 的 Webpack 配置](https://blog.csdn.net/qq_22889599/article/details/79507721)


### How to rewire your create-react-app project

#### 1) Install react-app-rewired

`$ npm install react-app-rewired --save-dev`

#### 2) Create a config-overrides.js file in the root directory

```
/* config-overrides.js */

module.exports = function override(config, env) {
  //do stuff with the webpack config...
  return config;
}
```

```
+-- your-project
|   +-- config-overrides.js
|   +-- node_modules
|   +-- package.json
|   +-- public
|   +-- README.md
|   +-- src

```

#### 3) 'Flip' the existing calls to react-scripts in npm scripts

```
  /* package.json */

  "scripts": {
-   "start": "react-scripts start",
+   "start": "react-app-rewired start",
-   "build": "react-scripts build",
+   "build": "react-app-rewired build",
-   "test": "react-scripts test --env=jsdom",
+   "test": "react-app-rewired test --env=jsdom"
}
```
#### 4) Start the Dev Server

```
$ npm start
```
#### 5) Build your app

```
$ npm run build
```
[react-app-rewired使用](https://github.com/timarney/react-app-rewired#3-flip-the-existing-calls-to-react-scripts-in-npm-scripts)