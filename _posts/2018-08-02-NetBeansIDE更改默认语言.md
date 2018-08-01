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


Dawson Lee edited this page on Beijing, 2018/8/2

<div class="breaker"></div>

  [1]:  /assets/posts/NetBeansIDE更改默认语言/找到netbeans.conf.PNG

## 更改默认语言为英语

*  1.找到`netbeans.conf`配置文件，推荐使用NetBeans IDE`文件->打开文件`打开文件netbeans.conf

![netbeans.conf配置文件][1]

*  2.给配置文件**添加**下面**字段**

在
	
	#netbeans_default_options="-J-client -J-Xss2m -J-Xms32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true"



中加上` -J-Duser.country=US`变为

		
	#netbeans_default_options="-J-Duser.country=US -J-client -J-Xss2m -J-Xms32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true"



**注意**：该字段在原本的文件中并不存在，您需要自己添加，保存后，重启IDE

## 更改默认语言为其它语言

*  中文

        -J-Duser.country=CN

*  日文 

        -J-Duser.country=JP

