---
layout: post
star: false
projects: true
category: projects
; category: blog
image: 
headerImage: false

title: "Taonomy Tool部署新版本指南"
date: 2018-10-4
author: dawsonlee
tag:
- tagName

---

  [1]: https://dev.mysql.com/downloads/workbench/
  [2]: /assets/posts/2018-10-4-Taonomy Tool部署新版本指南/connectdl03.png
  [3]: /assets/posts/2018-10-4-Taonomy Tool部署新版本指南/tag.png
  [4]: /assets/posts/2018-10-4-Taonomy Tool部署新版本指南/ducks.png


1. 使用[Mysql WorkBench 6.3.10][1]
2. 连接`dl03`中的mysql

    * hostname: `dl03`
    * port: `3306`
    * user name: `root`
    * password: `greathulu`
    ![connectdl03][2]

3. 修改`taxonomy`数据库的一些数据
    * 将`tag.best_score`的`datatype`改为`DOUBLE`
    * 将`tag.error_rate`的`datatype`改为`DOUBLE`
        ![tag][3]
    * 将'tag'中的'ducks, geese and swans'改为'ducks and geese and swans'
        ![ducks][4]
        * 此处修改数据的原因: 主要是为了在的`tag_score.xls`中可以被选择
        * 如果不修改,则对于TAG(tagName='ducks, geese and swans')不能使用 **分析数据** 和 **更新Tag数据** 的功能,但不会报错

4. 使用用户'jenkins'登陆'dl03'服务器

        jenkins@dl03

5. 取消taxonomy tool对应的docker容器

        $ sudo docker ps
            
    找到与dawsonlee1790/taxonomy:dl03相关的容器,然后使用命令停止运行该容器

        $ sudo docker container stop 容器ID

    使用命令部署新的版本(下面的命令我有些记不太清楚,如果报错,可以按箭头上去查看我之前的类似操作)

        $ sudo docker run -itd --net=host dawsonlee1790/taxonomy:3.0

        