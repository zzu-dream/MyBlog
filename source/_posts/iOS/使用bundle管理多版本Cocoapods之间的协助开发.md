---
title:  使用bundle管理多版本Cocoapods之间的协助开发
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2016-06-11 16:17:22
---


一般在公司团队开发中，在使用Cocoapods的时候，会面临同事之间使用的pod版本不一致的问题。

由于不同版本的pod在执行pod install或者pod update的时候会改变 .xcodeproj 的格式 或为xml 或者 json。这样就会造成很难解决的冲突问题。

因此这里介绍一下如何高效便捷的统一我们的Cocoapods版本。

### Bundle：

Bundler是一个ruby环境下的一个gem。

使用 Bundler 的原理就是通过为每个项目指定特定的一个pod版本,使用这个版本来执行install或者update。

好处就是我们在安装多个pod版本的时候，根据不同的项目需求去执行pod命令的时候，不用手动去切换pod的版本。

安装：

```
gem install bundler
```

创建gemfile文件

cd 项目目录  

```
bundle init
```

这样, 与 `.xcodeproj` 同级的目录中就会多出一个 `Gemfile`文件。

在Gemfile里添加如下代码，指定pod版本

```
# frozen_string_literal: true
source "https://rubygems.org"

# gem "rails"
gem 'cocoapods', '0.39.0'
```

到这里已经安装完毕，使用起来也很简单 
在之前执行的命令前面加上 `bundle exec`就好了，如：

```
bundle exec pod install --verbose --no-repo-update

或者

bundle exec pod update --verbose --no-repo-update
```

### 本地cocoapods版本列举
可以通过 gem list --local | grep cocoapods 命令查看我们电脑上安装了哪些版本的 CocoaPods，并通过 pod --version 查看系统默认使用的那个版本。


[多个版本的 CocoaPods 的切换](https://www.jianshu.com/p/411003ac28e4)