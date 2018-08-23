---
title: "Javaee7 tutorial中构建duke-forest失败的解决方案"
layout: post
date: 2018-08-21
image: 
headerImage: false
tag:
- Javaee7 tutorial
star: false
projects: false
category: blog
author: dawsonlee
externalLink: false

---

  [1]: /assets/posts/javaee7构建duke-forest失败的解决方案/examples.png
  [2]: /assets/posts/javaee7构建duke-forest失败的解决方案/pom.xml.png
  [3]: /assets/posts/javaee7构建duke-forest失败的解决方案/build-duke-forest.png

##  错误代码
	dukes-payment ..................................... FAILURE [4.308s]
	...
	Failed to execute goal org.codehaus.cargo:cargo-maven2-plugin:1.4.4:redeploy (deploy) on project dukes-store: 
	Execution deploy of goal org.codehaus.cargo:cargo-maven2-plugin:1.4.4:redeploy failed: 
	GlassFish admin command failed: asadmin exited 1 -> [Help 1]

##  原因
由于不能找到Glassfish的正确路径导致的

##  解决方案
#### NetBeans8.2

默认glassfish安装路径为`C:\glassfish4`（windows系统）

####  1.打开项目` /javaee-tutorial/examples`

![打开example][1]

####  2.打开项目`javaeetutorial->项目文件->pom.xml`

![打开pom.xml][2]

####  3.找到类似代码

{% highlight xml %}
<profile>
        <id>windows</id>
        <activation>
                <os>
                        <family>windows</family>
                </os>
        </activation>
        <properties>
                <glassfish.home.prefix>c:/</glassfish.home.prefix>
                <glassfish.executables.suffix>.bat</glassfish.executables.suffix>
        </properties>
</profile>
{% endhighlight %}

####  4.添加`<glassfish.home>${glassfish.home.prefix}/glassfish4</glassfish.home>`
        
{% highlight xml %}
<profile>
        <id>windows</id>
        <activation>
                <os>
                        <family>windows</family>
                </os>
        </activation>
        <properties>
                <glassfish.home>${glassfish.home.prefix}/glassfish4</glassfish.home>
                <glassfish.home.prefix>c:/</glassfish.home.prefix>
                <glassfish.executables.suffix>.bat</glassfish.executables.suffix>
        </properties>
</profile>
{% endhighlight %}

####  5.启动JavaDB
####  6.启动GlassFish Server
####  7.鼠标右键项目`dukes-forest`构建
	
![构建][3]
