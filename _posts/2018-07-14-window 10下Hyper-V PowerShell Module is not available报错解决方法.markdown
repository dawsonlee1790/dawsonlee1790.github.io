---
title: "NetBeans8.2配置服务器"
layout: post
date: 2018-07-14
image: 
headerImage: false
tag:
- Docker
star: false
category: blog
author: dawsonlee
---

Dawson Lee edited this page on Beijing, 2018/7/14

---
  [1]:  https://blog.csdn.net/harxingxing/article/details/docker-machine-Windows-i386.exe
  [2]:  https://github.com/harxingxing/favorite/raw/master/docker/docker-machine-Windows-x86_64.exe


##  注意
文件替换后使用管理员权限打开cmd或powershell命令行，否则可能还不能用

##  本结内容
在win10使用docker-machine创建Hyper-v虚拟机时，返回了一个错误”Error with pre-create check: “Hyper-V PowerShell Module is not available”。

解决方法非常简单，原因是docker-machine程序的版本问题，替换成 v0.13.0版本即可，详细操作如下:

1.  下载0.13.0版本docker-machine命令。点击下载：[32位系统][1]或[64位系统][2]
2.  下载完毕后，改名并替换”C:\Program Files\Docker\Docker\resources\bin”目录下的“docker-machine.exe”的文件，原文件最好备份一下。
##  参考文档
[https://blog.csdn.net/harxingxing/article/details/80495841](https://blog.csdn.net/harxingxing/article/details/80495841)


