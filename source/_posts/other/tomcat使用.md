---
title:  tomcat
tags:  [tomcat]
categories:  [工具]
date:  2018-06-11 16:17:22
---


[Tomcat的目录结构详细介绍](https://blog.csdn.net/u012661010/article/details/73381599)

#### 运行

切换到`tomcat`所在的目录在终端执行如下命令：  
`bash bin/startup.sh` 用来启动`tomcat` 

然后直接`localhost:8080/` 就可以访问了

#### 文件放置

webapps目录用来存放应用程序，当tomcat启动时会去加载webapps目录下的应用程序。可以以文件夹、war包、jar包的形式发布应用


#### 修改http访问端口（默认为8080端口），将8080修改为tomcat不在使用的端口号

1、安装目录下的`conf`子目录中的`server.xml`文件 修改位置如下：

```
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

2、然后在关闭和重启操作

`bash bin/shutdown.sh` 用来关闭`tomcat`   
`bash bin/startup.sh` 用来启动`tomcat` 


#### 启动tomcat 服务报 The file is absent or does not have execute permission

1、在`linu`上部署好`tomcat`后，准备启动时报错：

Cannot find bin/catalina.sh 
The file is absent or does not have execute permission 

This file is needed to run this program 


2、解决办法：

对启动脚本添加执行权限

`chmod 777  *.sh`