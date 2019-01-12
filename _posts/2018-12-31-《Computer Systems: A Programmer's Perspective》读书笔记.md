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

  [1]: https://pan.baidu.com/s/1ty54ze88ZfPwFOKCaf3GPw
  [2]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/1-编译系统.png
  [3]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/1-存储器层次模型.png
  [4]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/1-计算机系统分层模型.png
  [5]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P55计算机系统提供的一些抽象表示.png
  [6]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/1-进程的上下文切换.png
  [7]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/1-进程的虚拟地址空间.png
  [8]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-进制对照表.png
  [9]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-大端法和小端法.png
  [10]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-生成一张ascii表.png
  [11]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-布尔运算.png
  [12]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-位向量.png
  [13]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-子集.png
  [14]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-无符号二进制.png
  [15]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/2-二进制和二进制补码.png
  [17]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P64-T2U.png
  [18]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P64-二进制补码到无符号数的转换.png
  [19]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P114单精度浮点数值.png
  [20]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P150不理解的地方.png
  [21]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P155C语言数据类型在x86-64中的大小.png
  [22]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P200运行时栈.png
  [23]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P200错误.png
  [P157]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P157操作数格式.png
  [P165]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P165整数算术操作.png
  [P165-error]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P165错误.png
  [P173]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P173-SET指令.png
  [P176]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P176页错误.png
  [P188]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P188-jump_to_middle.png
  [P190]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P190-guarded-do翻译方法.png
  [P192]: /assets/posts/2018-12-31-Computer_Systems_A_Programmer's_Perspective_读书笔记/P192-for循环.png


## 书中存在的错误

* P150页（书本：114页）错误：![][20]
    * 应该是256TB
* P165页（书本：129页）错误：
    * 这里的操作顺序和ATT格式的汇编代码相反？应该是相同的吧
    * ![][P165-error]
* P176页（书本：140页）错误：
    * 红线标注部分应该是32位机器的内容，x86-64使用的应该是48位长的虚拟地址长度
    * 所以应该改为，1，2，4或8字节，然后使用8个字节直接指定目标（？？？我也不确定正确应该是怎样）
    * ![][P176]
* P200页（书本：164页）错误：![][23]
    * 应该是stack frame


## 简介

我读的是《Computer Systems:A programmer's Perspective》的中文翻译版[《深入理解计算机系统》][1]
    
* 密码:`3hrt`

## Chapter 1: 计算机系统漫游

* 本书的目的就是帮助程序员理解当执行hello world程序时，操作系统到底发生了什么以及为什么会这么会如此运作

* 在unix系统上，从源文件到可执行目标文件（executable object file）是由编译器驱动程序（compiler driver）
完成的



    unix> gcc -o hello hello.c
    
上述过程是gcc读取源程序文件hello.c，并翻译成可执行目标文件hello。这个翻译过程是分四个阶段完成的。

预处理器（cpp）-> 编辑器（ccl）-> 汇编器（as）-> 链接器（ld）

![编译系统][2]

* `.s`也称汇编文件
* `.o`也称目标代码文件 

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

#### 2.1.3 寻址和字节顺序

* 小端法（little endian）

* 大端法（big endian）

![大端法和小端法][9]

#### 2.1.4 表示字符串

* C中的字符串为一个以null（其值为零）字符结尾的字符数组

* 文本数据比二进制数据具有更强的平台独立性
    * 原因：对使用同一编码格式（例：ASCII码）的任意系统得到的数据结果都是一样的，与字节顺序和字大小规则无关
    
* 生成异常ascii码表


    unix> man ascii
    
![生成一张ascii表][10]


* java使用unicode来表示字符串

#### 2.1.5 表示代码 

* 二进制代码很少能在不同的机器和操作系统之间移植

* 程序仅仅只是二进制序列


#### 2.1.6 布尔代数和环（！！！）

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

#### 2.1.7 C中的位级运算

> 练习题2.10 ???
第一步：*x = a^b , *y = b
第二步：*x = a^b , *y = a
第三步：*x = b , *y = a

> 练习题2.12
x|m
x&m

#### 2.1.8 C中的逻辑运算

    &&, ||, !
    
> 练习题2.14
!(x^y)

#### 2.1.9 C中的移位运算

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

* 二进制反码（ones' complement）：P61
* 符号数值（sign-magnitude）：P61

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
    
#### 2.2.3 补码编码
    
#### 2.2.4 有符号和无符号数之间的转换(!!!)

* T2U中的T为Two's-complement,U为Unsigned

![P64-T2U.png][17]

![P64-二进制补码到无符号数的转换][18]

#### 2.2.5 C中的有符号与无符号数

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

#### 2.2.6 拓展一个数字的位表示

* 零拓展（zero extension）
    * 将一个无符号整数拓展成一个更大的数据类型，高位补0

* 符号拓展（sign extension）
    * 将一个二进制补码数拓展成一个更大的数据类型，高位补**符号位**
    
> 练习题：2.21
    * 127, 127
    * 128, -128
    * 255, -1
    * 0, 0
    
#### 2.2.7 截断数字

* `B2U_k([X_k-1, X_k-2, ..., X_0]) = B2U_w([X_w-1, X_w-2, ..., X_0]) mod 2^k`
* `B2T_k([X_k-1, X_k-2, ..., X_0]) = U2T_k(B2U_w([X_w-1, X_w-2, ..., X_0])) mod 2^k`

#### 2.2.8 关于有符号数和无符号数的建议

> 练习题 2.25 
    * 因为length - 1，当无符号数和有符号数进行运算时，机器自动将有符号数强制类型转换为无符号数，
    这就会造成length - 1 != 0，而是UMax_w
    * 修改为 (int)length - 1

> 练习题 2.26
    * 当s<t时 ？？？

* 事实上除了C以外很少有语言支持无符号数
    * Java中`>>`表示算术右移，`>>>`表示逻辑右移

### 2.3 整数运算

#### 2.3.1 无符号加法

* 大部分编程语言支持固定精度的运算，少部分编程语言支持无精度运算

> 练习题2.27
    
* 模数加法形成了一种数学结构，称为阿贝尔群（Abelian group）
    * 单位元0
    * 每个元素有一个加法逆元
    * 元素和它的加法逆元相加会等于单位元0

> 练习题2.28
    * 0, 0, 0
    * 5, 11, B
    * 8, 8, 8
    * 13, 3, 3
    * 15, 1, 1
    
#### 2.3.2 补码加法

#### 2.3.3 补码的非

> 练习题 2.33
    * 0, 0, 0
    * 5, 11, B
    * 8, 8, 8
    * 13, 3, 3
    * 15, 1, 1
    
* 补码非的位级表示！！！
    * 执行位级补码非的第一种方法是对每一位求补，再对结果加1
        * 在C中，-x和~x+1结果是一样的
    * 执行位级补码非的第二种方法是按从低位向高位的方向，将出现的第一个1**之后**的所有位求补
    
#### 2.3.4 无符号数乘法
#### 2.3.5 补码的乘法
#### 2.4.2 IEEE浮点表示

标准：`V = (-1)^s * M * 2^E

* 符号（sign）
* 尾数（significand）
* 阶码（exponent）

* 单精度格式

![单精度格式][19]

## Chapter3 程序的机器级表达

* 每个后继处理器的设计都是向后兼容的

* 摩尔定律
    * 半导体工业一直能使晶体管的数量每18个月翻一倍
    
#### 3.2.1 机器级代码

* 机器级编程有两种抽象特别重要
    * 第一种抽象：指令集架构（Instruction Set Architecture）
    * 第二种抽象：机器级程序使用的内存地址是虚拟地址

* x86-64的虚拟地址是64位的字
    * 在目前的实现中，高16位必须设为0。所以一个地址实际上能够指定的是2^48或64TB范围内的一个字节
    
* 程序计数器（通常称"PC"，在x86-64中用%rip表示）
    

#### 3.2 程序编码


* `linux> gcc -Og -o p p1.c p2.c`使用Og等级的优化将`p1.c`和`p2.c`翻译成可执行文件p
     * `Og`优化等级是GCC版本4.8之后引入的
     * `Og`优化等级是指编译器会生成符合原始C代码整体结构的机器代码的优化等级
        * 较高级别的优化产生的代码会严重变形

* `linux> gcc -Og -S mstore.c`使用Og等级的优化将`mstore.c`翻译成名为`mstore.s`的汇编文件

* `linux> gcc -Og -c mstore.c`使用Og等级的优化将`mstore.c`翻译成名为`mstore.o`的目标代码文件
    
* `linux> objdump -d mstore.o`反汇编器`objdump`将`mstore.o`目标代码文件反汇编成`mstore.s`汇编文件

* 旁注：ATT与Intel汇编代码格式
    * ATT是GCC、OBJDUMP和其他一些我们使用的工具的默认格式
    
#### 3.3 数据格式

![C语言数据类型在x86-64中的大小][21]

* 在64为机器中，指针长8字节！！！

#### 3.4 访问信息

* 整数寄存器

* 对于生成小于8字节结果的指令有相对应的两条规则
    * 生成1字节和2字节数字的指令会保持剩下的字节不变
    * 生成4字节数字的指令会把高位4个字节置为零
    
#### 3.4.1 操作数指示符

* 大多数指令有一个或多个操作数（operand）

* x86-64支持多种操作数格式
    * 立即数（immediate）：用来表示常数值
    * 寄存器（register）：表示某个寄存器的内容
    * 内存引用：它会根据计算出来的**有效地址**访问某个内存位置
    
![操作数格式][P157]
    
#### 3.4.2 数据传递指令

* x86-64加了一条限制，传送指令的两个操作数不能都指向内存位置
    * 将一个值从一个内存位置复制到另一个内存位置需要两条指令
    
#### 3.4.3 数据传送示例

#### 3.4.4 压入和弹出栈数据

#### 3.5 算术和逻辑操作

![P165整数算术操作][P165]

#### 3.5.1 加载有效地址（load effective address）

* `leaq`：加载有效地址（load effective address）
    * 实际上是`movq`指令的变形
    * 它的第一个操作数看上去是一个内存引用，但实际上它并没从指定的位置读入数据，而只是将有效地址写入到目的操作数
        * **疑问？**：那为什么当`%rdx=x`时执行`leaq 7(%rdx,%rdx,4),%rax`指令后，`%rax`表示`7+x+4x`
            * 解释：假设是执行`movq 7(%rdx,%rdx,4),%rax`表示的是第一个操作数计算得到的数是`7+x+4x`，然后将它作为
              有效地址，到虚拟内存中读取地址为`7+x+4x`对应的值，然后赋予`%rax`


#### 3.5.2 一元和二元操作

#### 3.5.3 移位操作

* 移位量可以是一个立即数（immediate），或者放在单字节寄存器%c1中。（这些指令很特别，
因为只允许以这个特殊的寄存器%c1作为操作数）

* 原则上来说一个字节的偏移量范围应该是 0 ～ 255 = 2^8 - 1。但在x86-64中，移位操作对w位长的数据值进行操作，
只会对低m位有效（2^m = w）。例如：指令salb会移7位，salw会移15位，sall会移31位，salq会移63位。

#### 3.5.5 特殊的算术操作

#### 3.6 控制

用jump指令可以改变程序运行的顺序，指令可能依赖于某一次测试的值。编译器必须产生构建在这种低级机制的指令序列，
来控制C语言的控制结构

#### 3.6.1 条件码

* 除了整数寄存器，CPU还维护着一组单个位的条件码（condition code）

* 最常用的条件码有
    * CF：进位标志
    * ZF：零标志
    * SF：符号标志
    * OF：溢出标志

* 两类指令：`CMP`和`TEST`指令，只会设置条件码（condition code）的值，不会更新寄存器中的值

#### 3.6.2 访问条件码

条件码（condition code）一般不会直接读取，它一般有三种使用方式

1. 根据条件码的某种组合，将一个字节设为0或1
2. 可以条件跳转到程序的某个其他的部分
3. 可以有条件的传输数据

![][P173]

#### 3.6.3 跳转（jump）指令

* `jmp`指令是无条件跳转
    * 直接跳转：即跳转目标是作为指令的一部分编码的
        * 例：`jmp .L1`
    * 间接跳转：从寄存器或内存位置中读出的
        * `jmp *%rax` : 用寄存器中的值作为跳转目标
        * `jmp *(%rax)`: 根据寄存器的值作为地址，从内存中读出跳转目标
        
#### 3.6.4 跳转指令的编码

我们不需要理解机器代码格式的相关细节，但了解跳转指令的目标如何编码十分重要

* 跳转指令有很多种编码方式
    * 最常见的是PC相对（PC-relative）寻址
        * 也就是会将目标指令的地址与紧跟在跳转指令后面的那条指令的地址之间的差作为编码 **！！！**，
        编码可以是1,2,4字节
    * 第二种编码方法：给出"绝对"地址
        * 用四字节直接给出目标地址
        
* 旁注：rep和repz是同义词
    * 作用：在AMD给编译器编写者的指导意见书中，建议用rep后面跟ret的组合来避免是ret指令成为条件跳转指令的目标

#### 3.6.5 用条件控制来实现条件分支（传统方式，低效）

将条件表达式翻译称机器代码，最常用的方式是有条件跳转和无条件跳转组合使用实现跳转

#### 3.6.6 用条件传送来实现条件分支（高效但非常局限）

但不是所有条件表达式都可以用条件传送来编译

GCC只有当分支中是两条加法的时候会使用条件传送，大部分情况下都会使用条件控制，虽然预测错误的开销很大

#### 3.6.7 循环

* 1.do-while循环

> 练习题3.23

> A. x -> %rdi, y -> %rcx, n -> %rdx

> B. 通过`leaq 1(%rcx,%rax),%rax`指令消除了对指针变量`p`和表达式`（*p）++`间接引用的需求

> C. 第4行：`compute y = x * x`
     第5行：`compute n = 2 * x`
     第7行：`compute x += y ; (*p)++`
     第9行：`compare n:n`
     第10行：`If n>0, goto .L2`
 
* 2.while循环

第一种翻译方法：jump to middle

![jump to middle][P188]

第二种翻译方法：guarded-do

![guarded-do][P190]

* 3.for循环

C语言标准说明，for循环与while循环的代码行为一样（有一个例外，使用continue时）

![for循环][P192]

#### 3.6.8 switch语句

* 多重分支（multiway switch）

* 跳转表（jump table）

* 标号（case label）

* C语言中`&`运算符创建一个指向数据值的指针
* C语言中`&&`运算符创建一个指向代码位置的指针

#### 3.7 过程

#### 3.7.1 运行时栈

![运行时栈][22]

* 栈帧（stack frame）
















