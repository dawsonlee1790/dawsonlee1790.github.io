---
layout: post
star: false
; projects: true
; category: projects
category: blog
image: 
headerImage: false

title: "《Java EE开发颠覆者：Spring Boot实战》读书笔记"
date: 2018-10-25
author: dawsonlee
tag:
- 读书笔记

---

  [1]: /assets/posts/***/***.png

## Spring技术栈
* IoC容器（ApplicationContext）
* AOP
* 数据访问
* Web开发
* 消息
* 测试

## spring的模块 
	在书的1.2

## Spring框架本身有四大原则
1. 实用POJO进行轻量级和最小侵入式开发
2. 通过依赖注入和基于接口编程实现松耦合
3. 通过AOP和默认习惯进行声明式编程
4. 实用AOP和模版（template）减少模式化代码

Inversion of Control-IOC 和 DI 在Spring里是等同的概念
Dependency Injection-DI 主要目的：解耦

声明Bean的注解
@Component组件，没有明确的角色
@Service在业务逻辑层（Service层）使用
@Repository在数据访问层（DAO层）使用
@Controller在展示层（MVC->Spring MVC）使用

注入Bean的注解，一般情况下通用
@Autowired：Spring提供的注解
@Inject：JSR-330提供的注解
@Resource：JSR-@250提供的注解

xml配置、注解配置、Java配置都是配置元数据
全局配置实用Java配置（如数据库相关配置、MVC相关配置）
业务Bean的配置实用注解配置（@Service、@Component、@Repository、@Controller）

AOP-Aspect Oriented Program
面向切面编程，相当于OOP面向对象编程
Spring的AOP的存在目的是为了解藕，AOP可以让一组类共享相同的行为。OOP中只能通过继承类和实现接口，增加了耦合度，AOP弥补了OOP的不足

Spring支持AspectJ的注解式切面编程

# 第二章 Spring常用配置

## 2.1 Bean的Scope

@Scope

* Singleton: 一个Spring容器只有一个Bean的实例，此为Spring 的默认配置，全容器共享一个实例
* Prototype：每次调用新建一个Bean的实例
* Request：Web项目中，给每个http request新建一个Bean实例
* Session：Web项目中，给每一个http session新建一个Bean实例
* GlobalSession：这个只在portal应用中有用，给每一个global http session新建一个Bean实例

## 2.2 Spring EL和资源调用

Spring主要在注解@Value的参数中实用表达式
1. 注入普通字符
2. 注入操作系统属性
3. 注入表达式运算结果
4. 注入其他Bean的属性
5. 注入文件内容
6. 注入网址内容
7. 注入属性文件

## 2.3 Bean的初始化和销毁

Spring对Bean的生命周期提供**Java配置**和**注解配置**两种方式的操作支持

1. Java配置方式：使用@Bean的initMethod和desrtoyMethod（相当于xml配置的ubut-method和destroy-method）
2. 注解方式：利用JSR-250的@PostConstruct和@PreDestroy
    * @PostConstruct，在构造函数执行完之后执行
    * @PreDestroy，在Bean销毁之前执行

## 2.4 Profile

Profile为在不同环境下使用不同的配置提供了支持（开发环境下的配置和生产环境下的配置肯定是不同的，例如，数据库的配置）

1. 通过设定Enviroment的actionProfiles来设定当前context需要使用的配置环境。在开发中使用@Profile注解类或者方法，达到在不同情况下选择实例话不同的Bean
2. 通过设定jvm的spring。profiles。active参数来设置配置环境。
3. Web项目设置在Servlet的context parameter中

## 事件（Application Event）

Spring的实践（Application Event）为Bean与Bean之间的消息通信提供了支持

Spring的事件需要遵循如下的流程
1. 自定义事件，集成ApplicationEvent
2. 定义事件的监听器，实现ApplicationListener
3. 使用容器发布事件

# Spring高级话题

## 3.1 Spring Aware

Spring的DI-Dependency Injection的最大亮点就是你的所有Bean对Spring容器的存在是没有意识的。即你可以将你的容器替换成别的容器，如Google Guice，这时Bean之间的耦合度很低。

但在实际项目中，如果你要使用Spring容器的资源，这时候Bean必须知道Spring容器的存在。这就是所谓的**Sping Aware**。若使用了Spring Aware，你的Bean将会和Spring框架耦合。

## 3.2 多线程

Spring通过任务执行器（TaskExecutor）来实现多线程和并发编程。使用ThreadPoolTaskExecutor可实现一个基于线程池的TaskExecutor。而世纪开发中任务一般是异步的，所以我们要在配置类中痛殴@EnableAsync开启对一步任务的支持，并通过在世纪执行Bean的方法中使用@Async注解来声明其是一个异步任务。

## 3.3 计划任务

配置类@EnableScheduling
执行计划任务的方法上注解@Scheduled

Spring通过@Scheduled支持多种类型的计划任务，包含cron、fix、Delay、fixRate等

## 3.4 条件注解@Conditional

## 3.5 组合注解与元注解

    @Target(ElementType.RUNTIME)
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Configuration
    @ComponentScan
    public @interface WiselyConfiguration{
      String[] value() default{};
    }

# 第四章 Spring MVC基础

## 4.1 Spring MVC概述

* MVC：Model+View+Controller（数据模型+视图+控制器）
* 三层架构：Presentation tier+Application tier+Data tier（展示层+应用层（Service层）+数据访问层（DAO层））

MVC只存在三层架构的展示层，M实际上数据模型，是包含数据的对象。（本人的小思考：是否可以理解为DTO-Data Transfer Object）

## 4.2 Spring MVC项目快速搭建

* 在Servlet 3.0+中，在SpringMVC里实现WebApplicationInitializer接口便可实现等同于web.xml的配置。
* ViewResolver这是SpringMVC视图（JSP下就是html）渲染的核心机制

# 第五章 Spring Boot概述

# 第六章 Spring Boot基础

## 6.5 Spring Boot运行原理

# 第七章 SpringBoot的Web开发

## 7.2 Thymeleaf模版引擎

## 7.3 Web相关配置

## 7.4 Tomcat配置

## 7.5 Favicon配置

## 7.6 WebSocket

* 通过@EnableWebSocketMessageBroker注解开启使用STOMP协议来传输基于代理（message broker）的消息

## 7.7 基于Bootstrap和AngularJS的现代Web应用

# Spring Boot的数据访问

## 8.1 引入Docker

## 8.2 Spring Data JPA

