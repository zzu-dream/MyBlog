
---
title: RN脚手架初始化项目在0.45版本后问题
tags: ReactNative学习
categories: ReactNative
date:  2018-06-15 16:17:22
---



由于 `RN 0.45.0` 后，需要依赖一些第三方库，这些库通过 npm 或 yarn 下载非常慢，所以可以先手动下载，放到此文件夹： `~/.rncache`（如果路径不存在就手动创建一个）

首先配置npm镜像 [地址跳转]() 如果依然失败的话 需要看以下步骤了。

以下是我用到的几个库（版本可能会有更新），如果手动下载有困难，可以找已经下载好的同学拿一下：

```
boost_1_63_0.tar.gz
double-conversion-1.1.5.tar.gz
folly-2016.09.26.00.tar.gz
glog-0.3.4.tar.gz
```

react更新依赖的脚本在这个地方：`react-native/scripts/ios-install-third-party.sh`

[百度网盘](https://pan.baidu.com/s/1kVDUAZ9#list/path=%2Fother%2Freactnative.cn%2Frn-third-party&parentPath=%2Fother%2Freactnative.cn)  
[外链下载](https://blog.csdn.net/u013751625/article/details/75046147)  
[iOS RN 0.45以上版本所需的第三方编译库(boost等)](https://bbs.reactnative.cn/topic/4301/ios-rn-0-45%E4%BB%A5%E4%B8%8A%E7%89%88%E6%9C%AC%E6%89%80%E9%9C%80%E7%9A%84%E7%AC%AC%E4%B8%89%E6%96%B9%E7%BC%96%E8%AF%91%E5%BA%93-boost%E7%AD%89)


产生原因：

* ~/.rncache 中 boost_1_63_0.tar.gz， double-conversion-1.1.5.tar.gz， folly-2016.09.26.00.tar.gz， glog-0.3.4.tar.gz 文件下载不完整

* node_modules/react-native/third-party 文件不完整

解决方案：

* 删除 .rncache 后重新下载，或手动下载后放入 .rncache 中

* 把以上文件解压后放入 node_modules/react-native/third-party 下
