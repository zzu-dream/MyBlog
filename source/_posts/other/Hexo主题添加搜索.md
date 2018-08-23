---
title:  Hexo 博客框架添加搜索
tags:  [博客框架]
categories:  [工具]
date:  2018-06-11 16:17:22
---


用Hexo提供的`Local Search`,原理是通过`hexo-generator-search`插件在本地生成一个`search.xml`文件，搜索的时候从这个文件中根据关键字检索出相应的链接。

### 安装步骤
##### 安装 hexo-generator-search

在站点的根目录下执行以下命令：


```
$ npm install hexo-generator-search --save
```

##### 安装 hexo-generator-searchdb

在站点的根目录下执行以下命令：

```
$ npm install hexo-generator-searchdb --save
```

启用搜索

编辑 站点配置文件`_config.yml`，新增以下内容到任意位置：

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```  

修改主题配置文件

我的路径：`/blog/themes/next`下的`_config.yml`文件，进行编辑。

```  
local_search:
    enable: true
```      


最后部署到github、coding，打开网页就可以看到搜索功能了。