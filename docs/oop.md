# 面向对象编程

## 概念

### dependency-inversion 依赖反转
通过抽象让软件以前的高层依赖底层代码反转成的底层依赖高层。抽象在代码里的实现通常是通过抽象类，或者接口(interface)

### dependency Injection 依赖注入 
简称DI，注意不要和依赖反转混淆。
就是在对象初始化的时候传入它的所有依赖。可以用来实现IoC和dependency-inversion