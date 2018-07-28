---
title: "NetBeans无法使用编码GBK安全地打开该文件的解决方法"
layout: post
date: 2018-07-28
image: 
headerImage: false
tag:
- NetBeans8.2
star: false
category: blog
author: dawsonlee
---

Dawson Lee edited this page on Beijing, 2018/7/28

<div class="breaker"></div>

   [1]:  /assets/posts/NetBeans无法使用编码GBK安全地打开该文件的解决方法/找到netbeans.conf.PNG


##  设置窗口字体大小


*  1.找到`netbeans.conf`配置文件
![netbeans.conf配置文件][1]

*  2.给配置文件**添加**下面**字段**

在

		
#
netbeans_default_options="-J-client -J-Xss2m -J-Xms32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true"



最后加上` -J-Dfile.encoding=UTF-8`变为

		
#
netbeans_default_options="-J-client -J-Xss2m -J-Xms32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true -J-Dfile.encoding=UTF-8"



**注意**：该字段在原本的文件中并不存在，您需要自己添加，保存后，重启IDE


