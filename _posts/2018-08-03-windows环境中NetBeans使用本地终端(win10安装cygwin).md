---
title: "windows环境中NetBeans使用本地终端(win10安装cygwin)"
layout: post
date: 2018-08-03
image: 
headerImage: false
tag:
- NetBeans8.2
- cygwin
- windows
star: false
category: blog
author: dawsonlee

---

  [1]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/本地终端需要cygwin.png
  [2]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/choose_installation_type.png
  [3]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/choose_installation_directory.png
  [4]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/select_local_package_directory.png
  [5]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/select_connection_type.png
  [6]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/choose_download_site.png
  [7]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/select_packages.png
  [8]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/添加环境变量.png
  [9]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/成功cmd.png
  [10]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/成功netbeans.png
  [11]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/参考netbeans.org.png
  [12]:  /assets/posts/windows环境中NetBeans使用本地终端(win10安装cygwin)/参考windows安装cygwin教程.png

##  本地终端需要cygwin的提示

![本地终端需要cygwin][1]

#  win10下安装cygwin

#### 1.我们可以到Cygwin的官方网站下载Cygwin的安装程序，地址是：

[http://www.cygwin.com/](http://www.cygwin.com/)

#### 2.下载完成后，运行setup.exe程序，出现安装画面。直接点“下一步”，出现安装模式的对话框，如下图所示：

![选择安装模式][2]

我们看到有三种安装模式：

*  Install from Internet，这种模式直接从Internet安装，适合网速较快的情况；
*  Download Without Installing，这种模式只从网上下载Cygwin的组件包，但不安装；
*  Install from Local Directory，这种模式与上面第二种模式对应，当你的Cygwin组件包已经下载到本地，则可以使用此模式从本地安装Cygwin。

从上述三种模式中选择适合你的安装模式，这里我们选择第一种安装模式，直接从网上安装，当然在下载的同时，Cygwin组件也保存到了本地，以便以后能够再次安装。选中后，点击“下一步”。

#### 3.选择Cygwin的安装目录，以及一些参数的设置。默认的安装位置是C:\cygwin\，你也可以选择自己的安装目录，然后选择“下一步”

![选择安装目录][3]

#### 4.选择安装过程中从网上下载的Cygwin组件包的保存位置，选择完以后，点击“下一步”

![选择组件包保存位置][4]

#### 5.选择网络连接的方式

![选择连接方式][5]

*  Use HTTP/FTP Proxy: 你可以自己使用自己的代理服务器进行网络连接

#### 6.选择镜像

![选择镜像][6]

国内用户可以选择阿里云镜像（**镜像我并没有测试过**）

[http://mirrors.aliyun.com/cygwin/](http://mirrors.aliyun.com/cygwin/) 

如果上一步中你是通过代理服务器**科学上网**的话无所谓选择什么镜像啦 

#### 7.选择需要下载安装的组件包

这里是通过**[参考文章](#reference)**知道的所需要的组建包：

*  binutils 
*  gcc
*  gcc-mingw
*  gdb
*  make

![组建包][7]

#### 8.之后便是下一步直到完成

#### 9.设置环境变量

![设置环境变量][8]

我的cygwin的bin地址是：`D:\cygwin64\bin`

#### 10.验证成功

1.  通过在Windows命令提示符下键入以下命令来检查Cygwin环境的版本：

        C:\> cygcheck -c cygwin

2.  通过在Windows命令提示符下键入以下命令，检查Cygwin gcc和g ++编译器，make和gdb的版本：

        C:\> gcc --version
        C:\> g++ --version
        C:\> make --version
        C:\> gdb --version

![成功cmd][9]

![成功netbeans][10]






<a id="reference"></a>
#### 参考

*  参考1：[Configuring NetBeans IDE 8.0 for C/C++/Fortran](https://netbeans.org/community/releases/80/cpp-setup-instructions.html#cygwin) 

![参考netbeans.org][11] 

*  参考2：[windows 安装cygwin教程](https://blog.csdn.net/chunleixiahe/article/details/55666792) 

![参考windows安装cygwin教程][12]