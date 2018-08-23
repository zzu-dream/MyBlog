---
title:  ESLint安装使用流程
tags: ESLint
categories: React
date:  2018-06-14 16:17:22
---
ESLint安装使用流程

# 京东通天塔项目安装使用流程

```
> 京东通天塔项目已经添加了相关的配置只需要做以下操作即可使用：
1. npm run install_eslint_packages     安装相关依赖包
2. IDE配置：
  http://139.199.180.74/showdoc/Public/Uploads/2017-12-12/5a2f4a15bfbcd.jpeg
3.输出使用 详见最底部 `ESLint输出报告方式`

```

# 新项目安装使用流程
## ESLint流程梳理

### 一、背景介绍
##### ESLint是一个用来识别 ECMAScript 并且按照规则给出报告的代码检测工具，使用它可以避免低级错误和统一代码的风格。ESLint被设计为完全可配置的，主要有两种方式来配置ESLint：
```
在注释中配置：使用JavaScript注释直接把配置嵌入到JS文件中。
配置文件：使用下面任一的文件来为全部的目录和它的子目录指定配置信息。
javascript：使用.eslintrc.js文件并导出一个包含配置的对象。
YAML：.eslintrc.yaml或者.eslintrc.yml
JSON：.eslintrc.json，并且此文件允许使用JS形式的注释
废弃的用法：.eslintrc，此文件可以是JSON或者YAML
package.json：在package.json文件中创建eslintConfig属性，所有的配置包含在此属性中。
这些文件的优先级则是按照以上出现的顺序
（.eslintrc.js > .eslintrc.yaml > .eslintrc.yml > .eslintrc.json > .eslintrc > package.json）。

三种方法可以配置ESLint
    > 使用.eslintrc.*文件（ 支持JSON和YAML两种语法）
    > 在package.json中添加eslintConfig配置块
    > 使用JavaScript注释直接把配置嵌入到文件中

可以被配置的信息主要分为3类：

Environments：你的 javascript 脚步将要运行在什么环境（如：nodejs，browser，commonjs等）中。
Globals：执行代码时脚步需要访问的额外全局变量。
Rules：开启某些规则，也可以设置规则的等级。 
```


### 二、作用
```
EsLint提供以下几种校验：

语法错误校验
不重要或丢失的标点符号，如分号
没法运行到的代码块（使用过WebStorm的童鞋应该了解）
未被使用的参数提醒
漏掉的结束符，如}
确保样式的统一规则，如sass或者less
检查变量的命名
```

### 三、安装 
```
安装

全局安装
npm i -g eslint
局部安装（推荐）
npm i -D eslint
安装完毕后，接下来新建一个配置文件.eslintrc.js，
或者使用如下的命令行来自动生成。

eslint --init

```

### 四、配置

##### 指定执行环境
```
JavaScript 代码可以运行在浏览器或 nodejs 等环境中，
每个环境的全局变量都不尽相同（如 nodejs 中没有 DOM 相关的全局变量）。
在配置文件中可以自由的指定执行环境。

// .eslintrc.js
module.exports = {
  env: {
    browser: true,
    node: true,
  },
};

https://eslint.org/docs/user-guide/configuring#specifying-environments
```
##### 指定全局变量
```
可以在配置文件或注释中指定额外的全局变量，false表明变量只读：

使用注释来配置：
/* global var1, var2 */
/* global var1:false, var2:false */
使用配置文件来配置：
// .eslintrc.js
module.exports = {
  globals: {
    var1: true,
    var2: true,
  },
};

```
##### 配置Rules
```
在配置文件中可以设置一些规则。

这些规则的等级有三种：

"off" 或者 0：关闭规则。
"warn" 或者 1：打开规则，并且作为一个警告（不影响exit code）。
"error" 或者 2：打开规则，并且作为一个错误（exit code将会是1）。

默认校验的地址http://eslint.org/docs/rules/
```


### 五、使用方法
```
通过命令行工具来使用 eslint 。
1、列出所有文件命令 eslint .
2、列出具体某个文件
eslint [options] file.js [file.js] [dir]
```
### 六、自动修复
```
eslint --fix [dir]
```

### 七、相关插件使用

##### ESLint输出报告方式

一、终端直接输出方式：
```
eslint .
```

二、md格式：(到eslint_report目录下查看md格式文件)
```
eslint run eslint_makdown 
```

三、html格式：（到eslint_report目录下查看html格式文件）
```
eslint run eslint_html
```

[test]: http://139.199.180.74/showdoc/Public/Uploads/2017-12-12/5a2f4a15bfbcd.jpeg "webstorm ESLint配置"
