---
title: "NetBeans导入Eclipse项目 由于两个IDE默认编码导致的中文乱码问题"
layout: post
date: 2018-08-05
image: 
headerImage: false
tag:
- Eclipse
- NeBeans
star: false
category: blog
author: dawsonlee

---

Dawson Lee edited this page on Beijing, 2018/7/14

---

  [1]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/导入项目.png
  [2]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/导入项目时忽略项目依赖关系.png
  [3]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/无法使用utf-8安全的打开.png
  [4]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/发现eclipse的默认编码是GBK.png
  [5]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/netbeans-gkb.png
  [6]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/reference1.png
  [7]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/取消勾选在编译时保存.png
  [8]:  /assets/posts/NetBeans导入Eclipse项目-由于两个IDE默认编码导致的中文乱码问题/右键清理并构建.png



##  NetBeans导入Eclipse项目

**温馨提示：请使用备份的项目进行操作**

![导入项目][1]

![导入项目时忽略项目依赖关系][2]
 
##  出现的问题

![无法使用utf-8安全的打开][3]

##  选择"是"以后发现中文乱码

**原因:发现eclipse的默认编码是GBK,而netbeans的默认编码是UTF-8**

![发现eclipse的默认编码是GBK][4]

##  然后

![netbeans-gkb][5]

**这个时候重新打开文件发现编译器中中文不再乱码**

但是新的问题又出现了:右键运行文件,输出还是乱码

**原因:编译的文件并没有更新**

但是这个时候`右键项目->清除并构建`后,运行文件输出还是乱码

**原因:**

![reference1][6]

[https://netbeans.org/kb/74/java/import-eclipse_zh_CN.html#build](https://netbeans.org/kb/74/java/import-eclipse_zh_CN.html#build) 

##  所以我们应该

![取消勾选在编译时保存][7]

##  最后`右键项目->清理并构建`

![右键清理并构建][8]

运行文件发现,中文乱码问题解决

