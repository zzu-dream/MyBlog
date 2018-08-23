---
title:  Hexo 博客框架
tags:  [博客框架]
categories:  [工具]
date:  2018-06-11 16:17:22
---


### 什么是 Hexo？
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
 
### 安装 Hexo
```
 $ npm install -g hexo-cli
```
### 建站
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### package.json
应用程序的信息。EJS, Stylus 和 Markdown renderer 已默认安装，您可以自由移除。

```
package.json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {
    "hexo": "^3.0.0",
    "hexo-generator-archive": "^0.1.0",
    "hexo-generator-category": "^0.1.0",
    "hexo-generator-index": "^0.1.0",
    "hexo-generator-tag": "^0.1.0",
    "hexo-renderer-ejs": "^0.1.0",
    "hexo-renderer-stylus": "^0.2.0",
    "hexo-renderer-marked": "^0.2.4",
    "hexo-server": "^0.1.2"
  }
}
```

### _config.yml
网站的 <a href="https://hexo.io/zh-cn/docs/configuration.html">配置</a> 信息，您可以在此配置大部分的参数。

### themes
 主题 文件夹。Hexo 会根据主题来生成静态页面。
 
### source

资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

### 重要的几个指令
了解更多 详见<a href="https://hexo.io/zh-cn/docs/commands.html#deploy">指令</a> 信息
>初始化新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站

```
$ hexo init [folder]  
```
>server 启动服务器。默认情况下，访问网址为： http://localhost:4000/。

```
$ hexo server
```
>generate 生成静态文件。

```
$ hexo generate
```

>deploy 部署网站。

```
$ hexo deploy
```

> clean 清除缓存文件 (db.json) 和已生成的静态文件 (public)。
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

```
$ hexo clean
```

### 资源文件夹
>资源（Asset）代表 source 文件夹中除了文章以外的所有文件，例如图片、CSS、JS 文件等。比方说，如果你的Hexo项目中只有少量图片，那最简单的方法就是将它们放在 source/images 文件夹中。然后通过类似于 
``` 
![](/images/image.jpg) 
```
>的方法访问它们。

### 部署
>Hexo 提供了快速方便的一键部署功能，让您只需一条命令就能将网站部署到服务器上。详见<a href="https://hexo.io/zh-cn/docs/deployment.html">网站</a> 信息
