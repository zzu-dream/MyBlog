---
title:  把json写入本地文件
tags:  [json文件中文乱码]
categories:  [Python]
date:  2017-05-19 16:17:22
---

## json中文ASCII乱码问题的解决
```py
* json中文ASCII乱码问题的解决
import sys
reload(sys)
sys.setdefaultencoding( "utf-8" )

```

## 判断路径是否存在(存在:True,不存在:False)
```py
def create_dir(path):
    # 去除首位空格
    path = path.strip()
    # 去除尾部 \ 符号
    path = path.rstrip("\\")
    isExists = os.path.exists(path)

    if not isExists:
        os.makedirs(path)
        print path + ' good 创建成功'
        return True
    else:
        print path + ' 该目录已存在拉'
        return False
```

## 删除文件

```py
def del_file(path):
    isExists = os.path.exists(path)
    if not isExists:
        return
    ls = os.listdir(path)
    for i in ls:
        c_path = os.path.join(path, i)
        if os.path.isdir(c_path):
            del_file(c_path)
        else:
            os.remove(c_path)

    shutil.rmtree(path)
```

## 将数据转换成字符串

```py
def test():
    test_dict = {'one': ['你好', {1: [['jd', 'hello'], ['cmo', 'china'], ['shanghai', 'mjgc']]}]}
    print(test_dict)
    print(type(test_dict))
    # dumps 将数据转换成字符串
    json_str = json.dumps(test_dict)
    print(json_str)
    print(type(json_str))
```  

## os模块popen方法 
> 可以直接使用终端的命令 例如：# 打开目录 open_path = 'open ' + output_dir_name
    os.popen(open_path)
[python调用shell命令](https://www.cnblogs.com/yangykaifa/p/7127776.html)    

```  py
popen方法可以得到shell命令的返回值。os.popen(cmd)后，
须要再调用read()或者readlines()这两个命令。输出结果。

 os.popen("ls")  
```  