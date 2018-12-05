---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "SpringBoot+Kotlin遇到的一些坑（持续更新）"
date: 2018-12-05
author: dawsonlee
tag:
- Spring Boot

---

  [1]: gradle.png

## Spring Data Jpa

当使用kotlin创建@Entity的DTO时，由于kotlin自身机制的原因：有了主构造函数之后就不会创建默认的构造函数了

#### 解决方法

项目中使用kotlin-jpa插件（gradle和maven都可以）

    build.gradle

![gradle][1]
![gradle2](gradle.png)