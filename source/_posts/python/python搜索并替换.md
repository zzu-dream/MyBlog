---
title:  搜索并替换
tags:  [搜索并替换]
categories:  [Python]
date:  2017-05-19 16:17:22
---


## 搜索并替换
```py
#!/usr/bin/python
# -*- coding: utf-8 -*-
import os
import imghdr
import re
suffix_list = ['m', 'h']
g_totalCount = 0
image_name = ''
def replace_in_path(filepath):
    global g_totalCount, image_name
    # print("Operation with : " + filepath)
    # open_file = open(filepath, 'r+') #用此种打开读写方式无效
    with open(filepath, 'r') as r:
        lines = r.readlines()
    with open(filepath, 'w') as w:
        for l in lines:
            r_pattern = r"\[\[Resources sharedResources\] getImageWithImageName:(.+?)\]"
            # if re.search(r_pattern, l):
            print '*******find*******'
            image_name_list = re.findall(r_pattern, l)
            if len(image_name_list):
                image_name = image_name_list[0]
                print("image_name:%s" % image_name)
            #
            replace_reg = re.compile(r_pattern)
            new_str = "JDImg(%s)" % image_name
            have_replace_string = replace_reg.sub(new_str, l)
            #
            w.write(have_replace_string)
    w.close()
def get_file_from_dir(dir):
    global g_totalCount
    for root, dirs, files in os.walk(dir):
        for item in files:
            filepath = os.path.join(root, item)
            # print 'filepath------%s' % filepath
            extension = os.path.splitext(filepath)[1][1:]
            if extension in suffix_list:
                replace_in_path(filepath)
                print '找到了------后缀为：[h or m]'
    print '###############结束##############'
if __name__ == '__main__':
    print "当前目录:%s" % os.getcwd()
    # 递归遍历目录下所有文件
    get_file_from_dir('/Users/wenyongjun/JD/JDiPad_git/JDiPad')
```