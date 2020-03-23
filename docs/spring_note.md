# Spring 官方文档中文笔记

更快地学习：英文好的话看[官方教学文档](https://docs.spring.io/spring/docs/5.2.x/spring-framework-reference/core.html#beans-dependencies)。有概念问题可以配合本站的概念解释一起食用

## 内容约定
- [?] 表示作者本人还没搞清楚的问题
- 章节顺序跟网站基本一致，但有些顺序因为理解而变动

## 1. IoC 容器

### 1.1 简介 IoC 容器 和 beans
IoC（控制反转）的新名字叫DI（依赖注入），指的是下面一串步骤(process)

首先，只通过下面三种方式定义对象的依赖：

- 构造函数参数
- factory method的参数
- 以及构造函数和 factory method 构造时设置的 properties

然后，当容器要创建`bean`的时候，就注入上面定义好的依赖

**什么是bean**

- spring 中通过 `IoC容器`管理的对象叫做`bean`
- 一个 `bean` 可以是已经被实例化，组装好的对象，也可以是`IoC容器`管理的还没组装的
- 也可以简单认为`bean`是你应用里的任意一个对象
- `bean`们和他们的依赖写在配置元数据里，`IoC容器`会使用这些配置去初始化`bean`

**继续说IoC容器**

最关键的代码在`org.springframework.beans` 和`org.springframework.context`，提供了spring的IoC 容器的基础。

`BeanFacory` interface 提供了先进的配置机制(比如xml配置文件）来管理各种`bean`

`ApplicationContext` interface 继承了`BeanFacory`， 增加了更多企业化的功能：

- 更容易集成AOP功能
- Message `Resources` 管理(用于国际化）[?]
- 事件发布[?]
- 应用层的特殊`context` 比如网络应用的`WebApplicationContext`

### 1.2 Container
