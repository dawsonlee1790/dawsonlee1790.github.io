---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "NetBeans创建能被Ant运行的build.xml"
date: 2018-09-28
author: dawsonlee
tag:
- Ant
- NetBeans

---

  [1]: /assets/posts/NetBeans创建能被Ant运行的build.xml/build.xml
  [2]: /assets/posts/NetBeans创建能被Ant运行的build.xml/模板管理器.png
  [3]: /assets/posts/NetBeans创建能被Ant运行的build.xml/新建build.xml.png
  [4]: /assets/posts/NetBeans创建能被Ant运行的build.xml/运行目标.png
  [4]: /assets/posts/NetBeans创建能被Ant运行的build.xml/运行结果.png

## 问题描述

NetBeans默认自带Ant工具，然而当我学习Ant并新建`build.xml`文件时，发现并不能直接使用
NetBeans自带的Ant运行文件。

## 解决方案

1. 下载[build.xml][1]
2. 工具->模板->选择下载的'build.xml'文件->添加

    ![模板管理器][2]

3. 选择 **收藏夹** （窗口->收藏夹;或者`ctrl+3`）任意文件夹,例如文件夹`Ant`
4. 右键->新建->其它
5. 在类别中选择`XML`
6. 在文件类型中选择`build.xml`

    ![新建build.xml][3]

7. 下一步->修改文件名称为`build`->完成
8. 选择 **收藏夹** 中文件夹`Ant`下新生成的`build.xml`文件
9. 右键->运行目标->info

    ![运行目标][4]

10. 在 **输出** 窗（窗口->输出;或者`ctrl+4`）中可以看到运行结果

    ![运行结果][5]