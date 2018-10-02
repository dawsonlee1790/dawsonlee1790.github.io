---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "NetBeans远程连接Centos7中docker"
date: 2018-10-02
author: dawsonlee
tag:
- NetBeans
- docker

---

  [1]: /assets/posts/2018-10-02-NetBeans远程连接Centos7中docker/daemon.png
  [2]: /assets/posts/2018-10-02-NetBeans远程连接Centos7中docker/添加Docker.png
  [3]: /assets/posts/2018-10-02-NetBeans远程连接Centos7中docker/配置URL.png

## 第一步:Centos7中Docker开启远程服务

1. 编辑`/usr/lib/systemd/system/docker.service`文件

        $ vim /usr/lib/systemd/system/docker.service

2. 在`[service]`部分加上下面两个参数

        [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H unix://var/run/docker.sock

    添加后效果如下

    ![daemon][1]

3. docker重新读取配置文件

        $ sudo systemctl daemon-reload

4. 启动docker服务

        $ sudo systemctl start docker

    如果原本已经启动则使用重启docker服务命令

        $ sudo systemctl restart docker

5. 查看docker进程，发现docker守护进程在已经监听2375的tcp端口

        $ ps -ef|grep docker

6. 查看系统的网络端口，发现tcp的2375端口，的确是docker的守护进程在监听

        $ netstat -tulp

7. (可以跳过)用另一台linux中的docker做客户端,去远程访问该centos7中的docker

        $ sudo docker -H tcp://192.168.196.141:2375 info

    * 这两台linux都是安装在vmware中的虚拟机
    * `192.168.196.141`是局域网的地址
    * 如果连接报错,注意检查centos7中的2375端口是否开启

## 第二步:NetBeans连接docker

1. 服务窗口(窗口->服务或者`ctrl+5`)中选择Docker,右键添加Docker

    ![添加Docker][2]

2. 配置名称->配置URL->测试连接->完成

    ![配置URL][3]

    * Tip:如果测试连接失败
        * 请检查centos7中的2375端口是否开启
        * **请检查NetBeans是否使用了代理服务器,导致不能连接VMware中的虚拟机**
