# Spring 官方文档中文笔记

更快地学习：英文好的话看[官方教学文档](https://docs.spring.io/spring/docs/1.2.9/reference/background.html)。有概念问题可以配合本站的概念解释一起食用

前两章是使用介绍和DI概念介绍，略过


## 3. Beans, BeanFactory and the ApplicationContext

### 3.1 介绍
最关键的代码在`org.springframework.beans` 和`org.springframework.context`，提供了spring的DI（又叫IoC）feature 的基础。

`BeanFacory` 提供了先进的配置机制(比如xml配置文件）来管理各种`bean（不清楚概念可以先理解为对象）`


### 3.2 BeanFactory 和 bean

`BeanFactory`是一个java容器，可以用来实例化、配置、管理`bean`。 这些`bean`通常互相写作，所以会有互相依赖。这些依赖反映(reflected)在`BeanFactory`使用的配置数据里。

它是一个`interface`，有很多实现，最常见的是`XmlBeanFactory`

它需要在代码中被实例化：
``` java
// 第一种方法
Resource res = new FileSystemResource("beans.xml");
XmlBeanFactory factory = new XmlBeanFactory(res);

// 第二种
ClassPathResource res = new ClassPathResource("beans.xml");
XmlBeanFactory factory = new XmlBeanFactory(res);

// 第三种
ClassPathXmlApplicationContext appContext = new ClassPathXmlApplicationContext(
        new String[] {"applicationContext.xml", "applicationContext-part2.xml"});
// 当然 ApplicationContext 其实也是一个 BeanFactory
BeanFactory factory = (BeanFactory) appContext;
```

XMLBeanFactory的配置文件长这样：
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN//EN" "http://www.springframework.org/dtd/spring-beans.dtd">

<beans>
  
  <bean id="..." class="...">
    ...
  </bean>
  <bean id="..." class="...">
    ...
  </bean>

  ...

</beans>
```

###
