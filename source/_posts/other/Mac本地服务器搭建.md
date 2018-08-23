---
title:  Mac端本地服务搭建
tags:  [启动本地服务]
categories:  [工具]
date:  2018-06-11 16:17:22
---


### 方案名称

Mac 系统 - 启用 Mac 本地 Web 服务器
关键字

Mac 系统 \ Web 服务器
### 需求场景

1. 局域网搭建 Web 服务器测试环境
参考链接

1. 简书 - Mac OS X 启用 Web 服务器(推荐)
详细内容 https://www.jianshu.com/p/d006a34a343f

### 启动 Apache

终端输入
$ sudo apachectl start
可启动 Apache，打开浏览器，输入 http://localhost/ 看到如下页面证明本地 Web 服务器启动成功


可启动 Apache，默认站点的根目录为系统级根目录
/Library/WebServer/Documents
更多信息，可参考 简书 - Mac OS X 启用 Web 服务器(推荐)

* 创建用户级根目录
* 启动 PHP
* 安装 MySQL
* 开启 HTTPS

https://github.com/viktyz/iosnotebook/blob/master/Notes/Note_00222_20170601.md


### 关闭和重启
Mac OS 终端起动、关闭、重启apache的方

Mac OS 终端起动、关闭、重启apache的方法



打开终端
重启apache：sudo /usr/sbin/apachectl restart
关闭apache：sudo /usr/sbin/apachectl stop
开启apache：sudo /usr/sbin/apachectl start
 