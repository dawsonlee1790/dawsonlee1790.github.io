---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "《Computer Systems: A Programmer's Perspective》读书笔记"
date: 2018-12-31
author: dawsonlee
tag:
- 读书笔记

---

  [1]: /assets/books/深入理解计算机系统.pdf
  [2]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-编译系统.png
  [3]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-存储器层次模型.png
  [4]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-计算机系统分层模型.png
  [5]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-操作系统提供的抽象表示.png
  [6]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-进程的上下文切换.png
  [7]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-进程的虚拟地址空间.png
  [6]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-进程的上下文切换.png
  [6]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-进程的上下文切换.png
  [6]: /assets/posts/2018-12-31-《Computer Systems: A Programmer's Perspective》读书笔记/1-进程的上下文切换.png


## 简介

我读的是《Computer Systems:A programmer's Perspective》的中文翻译版[《深入理解计算机系统》][1]

## Chapter 1: 计算机系统漫游

* 本书的目的就是帮助程序员理解当执行hello world程序时，操作系统到底发生了什么以及为什么会这么会如此运作

* 在unix系统上，从源文件到可执行目标文件（executable object file）是由编译器驱动程序（compiler driver）
完成的

        unix> gcc -o hello hello.c
    
上述过程是gcc读取源程序文件hello.c，并翻译成可执行目标文件hello。这个翻译过程是分四个阶段完成的。

预处理器（cpp）-> 编辑器（ccl）-> 汇编器（as）-> 链接器（ld）

![编译系统][2]

* shell是一个命令行解释器（一个应用程序）

#### 1.4.1 系统硬件组成

* 总线
    * 字（word）
    * 字长（字中的字节数）
    * 字节（8 byte）
* I/O设备
* 主存 
    * 物理上：主存是由一组DRAM（动态随机存取存储器）芯片组成的
    * 逻辑上：存储器是由一个线性的字节数组组成的，每个字节都有自己唯一的地址（数组索引） 
* 处理器（CPU）
    * 核心：一个被称为程序计数器（PC）的字长大小的存储设备（或寄存器）
    * 可能会执行的操作：
        * 加载
        * 存储
        * 更新
        * I/O读
        * I/O写
        * 转移
        
#### 1.4.2 - 1.7

* DMA(直接存储器存取)：数据可以不通过CPU而直接从磁盘到达主存

* 加快处理器的运行速度比加快主存的处理速度要容易和便宜得多

* 为了解决处理器和主存之间读取速度的差异，采用了高速缓存存储器（cache memories，简称高速缓存）

* L1和L2高速缓存是采用一种叫做**静态随机访问存储器**（SRAM）的硬件技术实现的
    
![存储器层次模型][3]

* 操作系统的两大功能：
    * 防止硬件被失控的应用程序滥用
    * 管理复杂而又广泛不同的低级硬件设备，给应用程序提供简单统一的接口
    
![计算机系统分层模型][4]
![操作系统提供的抽象表示][5]

* unix和posix标准

* **进程**
    * 进程是计算机科学中最重要和最成功的概念之一
    * 进程是操作系统对运行程序的一种抽象
    * 操作系统可以运行多个进程
    * 一个进程的指令和另一个进程的指令是交错进行的，我们称之为上下文切换（context switching）
    * 在任何时刻，都有且仅有一个进程正在运行
    * 实现线程需要低级硬件和操作系统软件的紧密合作
    
![进程的上下文切换][6]

* 线程
* 虚拟存储器
    * 虚拟存储器是一个抽象的概念
    * 它为每个进程提供一个假象，每个进程好像都在独占主存
    * 每个进程看到的存储器都是一致的，称之为**虚拟地址空间**
    * 先简单看看每一区
        * 程序代码和数据
        * 堆
        * 共享库
        * 栈
        * 内核虚拟存储器
    
![进程的虚拟地址空间][7]

* 文件：文件只不过就是字节序列
