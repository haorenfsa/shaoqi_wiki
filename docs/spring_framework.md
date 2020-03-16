# Spring Framework
现在互联网基本上java就跟spring框架绑死了，可以说不会spring就不敢说会java。

## Spring 是什么
它主要是java平台的 一种 应用框架 ，提供了[IoC](#ioc) 的[容器](#container)，它其实由很多模块构成。

## 构成模块
- Spring Core（**核心**）
    - utilities
    - [Bean](#javabean)容器

![image](https://docs.spring.io/spring/docs/1.2.9/reference/images/spring-overview.gif)

### IoC容器
是spring的核心容器，是spring的基础模块，提供了BeanFactory 和 ApplicationContext 。

## 概念

### JavaBean
`Java Beans` 是java里一些`类(class)`

- 他们的对象被叫做`bean`
- 这些类的一个对象里面封装了很多其它类的对象
- 他们可以被`序列化`
- 有一个无参数的构造函数
- 允许成员被getter setter访问
- 创造`bean`是为了写出容易复用的java应用组件

TODO:

### IoC 控制反转
Inversion of Controll 控制反转，是软件工程实践中的一条原则。

- 以前传统的[控制流](#controll-flow)是应用代码去调用框架来达成功能
- 而IoC是框架会按规则来调用应用代码，从而让应用达成功能。
- IoC使应用代码更模块化，更容易扩展。
- 它和事件驱动(event-driven)编程很有联系，事件驱动经常通过IoC实现：即，代码只关注处理事件，而事件管理和分派由框架实现。

跟它很相关的另一个概念是[依赖反转](/oop/#dependency-inversion), 是通过抽象让软件以前的高层依赖底层代码反转成的底层依赖高层。

我之前的理解是IoC可以通过依赖注入[DI]来实现，所以经常被混用。
实际上，依赖注入出处是作为是IoC更容易理解的说法：

In early 2004, Martin Fowler asked the readers of his site: when talking about Inversion of Control: "the question, is what aspect of control are they inverting?". After talking about the term Inversion of Control Martin suggests renaming the pattern, or at least giving it a more self-explanatory name, and starts to use the term Dependency Injection. His article continues to explain some of the ideas behind Inversion of Control or Dependency Injection. If you need a decent insight: http://martinfowler.com/articles/injection.html.

### controll flow 控制流
Flow of Controll 或者 controll flow，是指程序的语句、调用的执行顺序

### container容器
容器有多个含义:

#### 1. 存放数据的的container
当我们说spring是一个容器指的就是这个，就想java.util.List, Hash一样，是能存放一组数据的东西，只不过spring这个container里存放的是JavaBean。

#### 2.web container
当我们说Apache Tomcat是一个容器时，是指: web container，又叫servlet container

- 它是java网络服务的一个组件
- 它和java servlets们交互。
- 负责管理servelets们的生命周期。
- 把URL映射到servelet来保证请求正确执行。
- 实现了Java EE 架构中的网络组件约定


### servelet
一个小型的服务端程序，可以根据输入，自动生成响应。通常指HTTP servelet


### java servelet
java实现的servelet：流程是用户访问JSP页面，Tomcat或者Jetty翻译JSP,servelet的java实现代码被编译，然后执行并返回响应。
https://en.wikipedia.org/wiki/Java_servlet

### Java EE
Java Enterprise Edition，(Java EE), 以前被叫做 Java 2 Platform, Enterprise Edition (J2EE)，现在又叫Jakarta EE

- 它是一系列的正式约定[(specification)](#formal-specification)
- 扩展了java SE 8 (SE表示标准版)
- 增加的约定是关于企业会用到的分布式计算和网络服务
- 这些约定定义了API和API的交互


### JSP
https://en.wikipedia.org/wiki/JavaServer_Pages

### Formal specification正式约定
java的specification都是由[JCP](#jcp)机制定义的

计算机科学中广义的formal specification见：
https://en.wikipedia.org/wiki/Formal_specification

### JCP JSRs
JCP: Java Community Process

JCP是关于Java Specification Requests (JSRs)的。 

- JSRs是一些正式的文档.
- JSRs们描述了所有提出想要加入java平台的约定和技术
- JSR提出以后经过被大众review，并被JCP委员会通过后成为正式的。
- 最终的JSR会包含一个参考实现，一个kit来验证是否符合API约定。
- JSR定义了JCP自身，JSR 215 定义了当前的JCP 2.7

A JSR describes the JCP itself. As of 2009, JSR 215 describes the current version (2.7) of the JCP.

### AOP
TODO:


### MVC
TODO: