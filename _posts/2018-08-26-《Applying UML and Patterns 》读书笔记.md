---
title: "《Applying UML and Patterns》读书笔记"
layout: post
date: 2018-08-27
tag:
- 读书笔记
category: blog
author: dawsonlee

---

  [2.11]: /assets/posts/《Applying UML and Patterns》读书笔记/2.11-UP阶段.png
  [2.11-en]: /assets/posts/《Applying UML and Patterns》读书笔记/2.11-UP阶段-en.png
  [2.12]: /assets/posts/《Applying UML and Patterns》读书笔记/2.12-开发案例.png
     

## 第1章：绪论

#### OOAD（Object-Oriented Analysis and Design） & 迭代开发（Iterative Development）

#### OOD的原则和模式

* 原则：分配职责
* 职责驱动设计（responsibility-driven design）：经典OO设计之象征

## 第2章：迭代、进化和敏捷

迭代开发是OOAD成为最佳实践的核心。敏捷实践（如敏捷建模）是有效应用UML的关键。
UP是相对流行的、示范性的迭代方法。

#### 2.1 什么是UP & RUP？

UP是构造面向对象系统的迭代软件开发过程。描述了构造、部署以及维护软件的方式。

RUP是UP的详细精化。

* UP鼓励引进其他迭代方法的有效实践。例如：XP的重构，Scrum日常会议等实践
（不管黑猫还是白猫，抓到耗子的就是好猫）

* **UP可应用于敏捷方法**（XP或Scrum）

#### 2.2 迭代开发（interative development）（iterative and incremental development）
（interative and evolutionary development）

* 每一个迭代（3周）：都有**需求分析、设计、实现、测试**的活动
* **迭代是时间定量的**：关键思想

#### 2.5 风险驱动和客户驱动的迭代计划

UP（及大多数新方法）提倡 **风险驱动（risk-driven）** 和 **客户驱动（client-driven）** 
（用例驱动）相结合的迭代计划。

风险驱动迭代开发更明确地包含了 **以架构为中心（architecture-centric）** 迭代
开发的实践。意味着早期迭代要致力于核心架构的构造、测试和稳定。因为没有稳定的架构会
带来高风险。


#### 2.6 什么是敏捷方法

**敏捷开发**（agile development）方法通常是时间定量的迭代开发，提倡增量交付，提倡
**敏捷性** （快速灵活地响应变更）。

* 敏捷方法是不可能精确地定义的

#### 2.7 什么是敏捷建模（agile modeling）

**建模（构建UML草图等）的目的是为了来理解，而非文档。**

* “实行UML”（其真正含义为“实行OOAD”）的目的不是指设计者创建大量详细的UML图并递交
给编程者（这其实是非敏捷的和面向瀑布的思维方式）

#### 2.8 什么是敏捷UP

UP的创始人并没有为其赋予重量级或非敏捷的含义。实际上，UP可以采纳和应用可适应性和轻量级
的精神——敏捷UP。

*  使用UP活动和制品的简集

#### 2.10 **什么是UP的阶段**

四个主要阶段

1. 初始化（Inception）：大体构想、业务案例、范围和模糊评估
* 初始阶段不是需求阶段，而是研究可行性的阶段
2. 细化（Elaboration）：精化的构想、核心架构的迭代实现、高风险的解决、确定大多数的
需求和范围、更为实际的评估
* 细化阶段不是需求或设计阶段，而是迭代实现核心架构并解决高风险的阶段
3. 构造（Construction）：对遗留下来的低风险和简单元素进行迭代实现，准备部署
4. 移交（Transition）：进行beta测试和部署

#### 2.11 什么是UP科目

科目（descipline）：一组活动（及相关制品），例如需求分析中的活动。

制品（artifact）：工作产品的统称，如代码、模型、图等。

本书关注以下三个科目中的制品：

* **业务建模**： 领域模型制品
* **需求**： 用例模型及其补充性的规格说明制品。
* **设计**： 设计模型

![UP阶段][2.11]

![UP阶段-en][2.11-en]


#### 开发案例

![开发案例][2.12]

