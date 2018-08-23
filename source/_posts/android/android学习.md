---
title:  android学习
tags:  [android学习]
categories:  [android]
date:  2018-06-11 16:17:22
---


<!--2014、11、12-->

### Android 之 fill_parent 、wrap_content 、match_parent属性

`fill_parent` 设置一个顶部布局或控件为  
`fill_parent`将强制性让它布满整个屏幕。  
`wrap_content` 设置一个视图的尺寸为  
`wrap_content`将强制性地使视图扩展以显示全部内容

### 在程序中输出日志, 使用 android.util.Log 类. 

该类提供了若干静态方法   
Log.v(String tag, String msg);   
Log.d(String tag, String msg);   
Log.i(String tag, String msg);   
Log.w(String tag, String msg);   
Log.e(String tag, String msg);   
分别对应 Verbose, Debug, Info, Warning,Error.   
tag是一个标识,可以是任意字符串,通常可以使用类名+方法名, 主要是用来在查看日志时提供一个筛选条件.   
程序运行后 并不会在 ide的控制台内输出任何信息.   
如果要后查看日志 请使用   
adb logcat  

### 快捷键 
command + shift + f 格式化代码 ，option + / 提示，option + 上下键 移动某行代码，option + command + 上下键，option + command + s  弹出菜单功能页，Ctrl+1 快速修复(最经典的快捷键,就不用多说了)

### layout文件夹里新建xml命名

必须都是小写
  
### 完成A跳转到B操作：要在AndroidMainifest.xml的文件里面

``` java
 <activity
            android:name="com.example.sample1.新加入的类名字”
            android:label=“页面的标题” >
 </activity>
 
```     
   
AndroidManifest.xml是Android应用程序中最重要的文件之一。它是Android程序的全局配置文件，是每个 android程序中必须的文件。它位于我们开发的应用程序的根目录下，描述了package中的全局数据，包括package中暴露的组件 （activities, services, 等等），以及他们各自的实现类，各种能被处理的数据和启动位置等重要信息。
  

<!--2014、11、13-->

### 布局Layout管理

[布局](http://www.cnblogs.com/mengdd/archive/2012/12/19/2825382.html)  
 　
 　　布局即是指Activity中组件的呈现方式，即组件大小、间距和对齐方式等。  
　　Android提供了两种创建布局的方式：  
　　　　1.在XML配置文件中声明（推荐）。  
　　　　2.在程序中通过代码直接实例化布局及其组件。  
在Android中常见的布局方式：  
线性布局（LinearLayout）：按照垂直或者水平方向布局组件。  
　　帧布局（FrameLayout）：组件从屏幕的左上角坐标布局组件。  
　　表格布局（TableLayout）：按照行列方式布局组件。  
　　相对布局（RelativeLayout）：相对其他组件的布局方式。  
　　绝对布局（AbsoluteLayout）：按照绝对坐标来布局组件。（已废）。  
2、一个ListView通常有两个职责。  
（1）将数据填充到布局。  
（2）处理用户的选择点击等操作。  
第一点很好理解，ListView就是实现这个功能的。第二点也不难做到，在后面的学习中读者会发现，这非常简单。  
一个ListView的创建需要3个元素。  
（1）ListView中的每一列的View。  
（2）填入View的数据或者图片等。  
（3）连接数据与ListView的适配器。  
3、关于List<E>的用法  
List l=new List();  
 现在这样，如果你想放得是User类，就这样new:  
 List <User> l=new List <User>();  
 这样编译器就可以帮你监督，如果你往里面放其他类对象，就会报错咯。  
 当然好处就是你拿出来就是User类对象，不用再强制转换了。比如过去：  
 User u=(User)l.get(1);  
 现在就可以：  
 User u=l.get(1);  
4、ArrayList && HashMap 的使用 

``` java
 
 	ArrayList<HashMap<String,String>> list=new ArrayList<HashMap<String,String>>();  
        HashMap<String,String> map1= new HashMap<String,String>();  
        HashMap<String,String> map2= new HashMap<String,String>();  
        HashMap<String,String> map3= new HashMap<String,String>();  
          
        map1.put("user", "zhang");  
        map1.put("id", "192.168.0.0");  
          
        map2.put("user", "wang");  
        map2.put("id", "192.168.0.1");  
          
        list.add(map1);  
        list.add(map2);  
        list.add(map3); 
        
        Log.v("ArrayList==HashMap===:", list.toString());
        
``` 

### AlertDialog 的使用
 		 
``` java
		 
 		Builder alertDialog = new AlertDialog.Builder(this);
 		alertDialog.setTitle("标题");// 设置标题
 		alertDialog.setMessage("一个消息框");// 设置消息
 		alertDialog.setPositiveButton("确定", new DialogInterface.OnClickListener() {
 			
 			@Override
 			public void onClick(DialogInterface dialog, int which) {
 				// toast 的用法
 				Toast.makeText(getApplicationContext(), "你选择了确定",
 					    Toast.LENGTH_SHORT).show();
 			}
 		});
 		alertDialog.show();
 		
```		

### Button 的使用: 通过具体的id 找到某个控件

``` java
        // 给按钮加上点击事件
        clickMeButton.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                Log.v("click", "=======clickButton=======");
                // 跳转到SecondActivity页面
                Intent intent = new Intent();
                intent.setClass(MainActivity.this, SecondActivity.class);
                startActivity(intent);
            }
        });
        
```     

### dp是虚拟像素，在不同的像素密度的设备上会自动适配，比如:

在320x480分辨率，像素密度为160,1dp=1px
在480x800分辨率，像素密度为240,1dp=1.5px
计算公式:1dp*像素密度/160 = 实际像素数
px（像素）：屏幕上的点。
dp（与密度无关的像素）：一种基于屏幕密度的抽象单位。在每英寸160点的显示器上，1dp = 1px。
尽量使用dp作为空间大小单位，sp作为和文字相关大小单位 

 
