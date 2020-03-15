# Spring Framework
现在互联网基本上java就跟spring框架绑死了，可以说不会spring就不敢说会java。

## Spring 是什么
它是java平台的 一种 应用框架 以及 [IoC](#ioc) 的 [容器](#container)


## 概念

### IoC 控制反转
Inversion of Controll 控制反转，是软件工程实践中的一条原则。

- 以前传统的[控制流](#controll-flow)是应用代码去调用框架来达成功能
- 而IoC是框架会按规则来调用应用代码，从而让应用达成功能。

跟它很相关的另一个概念是[依赖反转](/oop/#dependency-inversion), 是通过抽象让软件以前的高层依赖底层代码反转成的底层依赖高层

### controll flow 控制流
Flow of Controll 或者 controll flow，是指程序的语句、调用的执行顺序

### container容器
容器有多个含义:

#### 1.web container
spring是container里 container是指: web container，又叫servlet container

- 它是网络的一个组件
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