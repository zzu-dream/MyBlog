---
title:  Xcode中如何去掉默认的Main.storyboard
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---

xcode 6取消了 Empty Application 模板来创建一个工程，创建出来的有工程多了Main.storyboard，默认加载Main.storyboard，但是有很多人还想用代码来实现UI的布局，去除Main.storyboard的有三步：

**修改**  

* 首先如图打开工程下面Supporting Files下面的Info.plist

	`Main storyboard file base name`删除这一行


* 其次找到工程的TAGETS/General/Deployment Info 删除Main。


* 经过上面两步算是删除了工程对Main.storyboard的依赖，但是运行工程后会发现是黑屏

在AppDelegate中的- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 中添加以下代码即可解决

```
self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
 self.window.backgroundColor = [UIColor whiteColor];
[self.window makeKeyAndVisible];
```

**报错**  

程序运行会提示：

```
Application windows are expected to have a root view controller at the end of application launch
```
**解决方案** 

意思是应用程序期望拥有一个根控制器（RootViewController）  
修改上面的代码，随便添加了一个控制器，程序就不抱错了

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    self.window.backgroundColor = [UIColor whiteColor];

    UITabBarController *tbc = [[UITabBarController alloc] init];

    self.window.rootViewController = tbc;

    [self.window makeKeyAndVisible];

    return YES;
}
```