---
title: "NetBeansIDE更改默认语言"
layout: post
date: 2018-08-02
image: 
headerImage: false
tag:
- NetBeans9.0
- NetBeans8.2
star: false
category: blog
author: dawsonlee

---



  [1]:  /assets/posts/NetBeansIDE更改默认语言/找到netbeans.conf.PNG

## 更改默认语言为英语

*  1.找到`netbeans.conf`配置文件，推荐使用NetBeans IDE`文件->打开文件`打开文件netbeans.conf

![netbeans.conf配置文件][1]

*  2.给配置文件**添加**下面**字段**

在
	
	#netbeans_default_options="-J-client -J-Xss2m -J-Xms32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true"



中加上`-J-Duser.language=zh -J-Duser.country=US`变为

		
	#netbeans_default_options="-J-Duser.language=zh -J-Duser.country=US -J-client -J-Xss2m -J-Xms32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true"

参数` -J-Duser.language=zh -J-Duser.country=US ` 是调用java的本身系统属性，设置语言为中文，国家为美国。这点很重要！

国家是美国使Netbeans的界面为英文，而语言为中文使Netbeans可以支持中文，如果只需要英文则可以把language设为en，不过在调用file browser的时候会发现左边一系列windows特性的中文按钮都回变成乱码。

**注意**：该字段在原本的文件中并不存在，您需要自己添加，保存后，重启IDE

## 更改默认语言为其它语言

*  中文

        -J-Duser.country=CN

*  日文 

        -J-Duser.country=JP

