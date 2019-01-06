---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "《Computer Systems: A Programmer's Perspective》读书笔记"
date: 2019-01-03
author: dawsonlee
tag:
- 读书笔记

---

  [1]: /assets/books/深入理解计算机系统.pdf
  [2]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/1-编译系统.png
  [3]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/1-存储器层次模型.png
  [4]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/1-计算机系统分层模型.png
  [5]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/1-操作系统提供的抽象表示.png
  [6]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/1-进程的上下文切换.png
  [7]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/1-进程的虚拟地址空间.png
  [8]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-进制对照表.png
  [9]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-大端法和小端法.png
  [10]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-生成一张ascii表.png
  [11]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-布尔运算.png
  [12]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-位向量.png
  [13]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-子集.png
  [14]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-无符号二进制.png
  [15]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/2-二进制和二进制补码.png
  [16]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/P64页错误.png
  [17]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/P64-T2U.png
  [18]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/P64-二进制补码到无符号数的转换.png
  [19]: /assets/posts/2018-12-31-《Computer_Systems:_A_Programmer's_Perspective》读书笔记/P67错误.png

## 书中存在的错误
* P64页：![P64页错误][16]
    * 两个等号之间的括号中的减号应该改为加号
* P67：红框我猜测是偏离了出题的原意，原意应该是-2147483647
    * ![P67错误][19]

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
    * 字节（8 bit）
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
        
#### 1.4.2 - 1.10

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

* 操作系统内核是硬件和系统软件之间的媒介

## Chapter 2 信息的表示和处理

![进制对照表][8]

* 字长（word size）
    * 指明整数和指针数据的标示大小（nominol size）
    * 对32位计算机来说，程序最多访问2^32字节，这就限制了虚拟地址空间为4GB

#### 2.1.4 寻址和字节顺序

* 小端法（little endian）

* 大端法（big endian）

![大端法和小端法][9]

#### 2.1.5 表示字符串

* C中的字符串为一个以null（其值为零）字符结尾的字符数组

* 文本数据比二进制数据具有更强的平台独立性
    * 原因：对使用同一编码格式（例：ASCII码）的任意系统得到的数据结果都是一样的，与字节顺序和字大小规则无关
    
* 生成异常ascii码表


    unix> man ascii
    
![生成一张ascii表][10]


* java使用unicode来表示字符串

#### 2.1.6 

* 二进制代码很少能在不同的机器和操作系统之间移植

* 程序仅仅只是二进制序列


#### 2.1.7 布尔代数和环（！！！）

* 二进制值是计算机编码、存储和操作信息的核心

* 布尔代数（bool algebra）
    * 起源：1850年左右乔治布尔（George Boole）的工作

![布尔运算][11]


* 整数环：`<Z, +, *, -, 0, 1>`
* 布尔代数：`<{0,1}, |, &, ~, 0, 1>`
* 整数环和布尔代数这两种数据结构大体上相同，但也有一些关键点不同，尤其是在`-`和`~`之间
* 布尔环：`<{0,1}, ^, &, /,>`
    * `/`：同一运算（identity operation）
    
> 练习题2.8
~a = 10010110
~b = 10101010
a & b = 01000001
a | b = 01111101
a ^ b = 00111100

* 位向量：![位向量][12]
    * 可以用向量表示任何子集![子集][13]

> 练习题2.9
A. 
黑 <-> 白
蓝 <-> 黄
绿 <-> 红紫
蓝绿 <-> 红
B.
???
C.
101
001
101

#### 2.1.8 C中的位级运算

> 练习题2.10 ???
第一步：*x = a^b , *y = b
第二步：*x = a^b , *y = a
第三步：*x = b , *y = a

> 练习题2.12
x|m
x&m

#### 2.1.9 C中的逻辑运算

    &&, ||, !
    
> 练习题2.14
!(x^y)

#### 2.1.10 C中的移位运算

    <<, >>

* `>>`:右移运算
    * 一般而言系统支持两种方式的右移运算
        * 逻辑右移：往左边补0
        * 算术右移：在左边补最高有效位的拷贝
            * 算术右移对有符号整数数据的运算非常有用
    * 一般而言：无符号（unsigned）整数必须使用逻辑右移，有符号整数使用算术右移

#### 2.2 整数表示

* C支持多种整形数据类型——表示有限范围的整数
    * char
    * short
    * int
    * long
    
* C/C++中支持无符号数和有符号数，Java只支持有符号数

* 有符号数的计算机表示：**二进制补码**（two's-complement）

* 无符号二进制![][14]

* 二进制到二进制补码![][15]

* 历史上存在过的有符号编码
    * 二进制反码
    * 符号数值
    
* 强制类型转换没有改变位的表示，改变的只是解释位的方式

> 练习题2.18
    * -8 = 8
    * -6 = 10
    * -4 = 12
    * -1 = 15
    * 0 = 0         
    * 3 = 3
    
#### 2.2.3 有符号和无符号数之间的转换(!!!)

* T2U中的T为Two's-complement,U为Unsigned

![P64-T2U.png][17]

![P64-二进制补码到无符号数的转换][18]

#### 2.2.4 C中的有符号与无符号数

* 显示强制转换
* 隐示强制转换

* 由于C同时包含有符号和无符号数的表达式的处理方式，会出现一些奇特的行为
    * 一个运算，有一个运算数是无符号的，另一个运算数是有符号的，那么C会隐示地将有符号参数强制转换为无符号数

> 练习题：2.20
    * 无符号 1
    * 有符号 0 (-2147483648在32位机器上会溢出，但会被机器识别成什么数字呢？)
    * 无符号 0
    * 有符号 1
    * 无符号 1


