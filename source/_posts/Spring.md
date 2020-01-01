---
title: Spring学习笔记
date: 2019-04-27 11:53:22
categories: spring
---
该文为记录和总结SSM三大框架的知识点。

### Spring介绍
Spring框架是一个开源的Java平台，同时也是最受欢迎的企业级Java应用程序开发框架。该框架的基础版本只有 2MB 左右的大小，是一个非常轻量级的框架。

#### 优点
判断框架是否优秀，看该框架是否为<font color = "#6298CE">**非侵入式**</font>，以及<font color = "#6298CE">**可扩展性**</font>、<font color = "#6298CE">**解耦性**</font>和<font color = "#6298CE">**开发周期**</font>等。
Spring的优点：
1. 有效地组织中间层对象，减少系统的可测试性和面向对象特性
2. 低浸入式，代码污染极低
3. 独立于各种应用服务器，基于Spring框架的应用
 
#### 核心
##### IOC/DI
IOC(Inversion of Control,控制反转)/DI(Dependency Injection,依赖注入)  
IOC是一种设计思想，控制反转意味着将设计好的对象交给容器控制，而不是传统的在对象内部直接控制。在程序运行中，系统动态的向某个对象提供所需的其他对象，这一点是通过DI实现的。依赖注入以Java反射机制为基础，把底层类作为参数传入上层类，实现上层类对下层类的“控制”。
- <font color = "#6298CE">IOC解耦图</font>
![IOC解耦](https://github.com/mzzzzzzzp/mzzzzzzzp.github.io/blob/master/images/IOC%E8%A7%A3%E8%80%A6.png?raw=true)

- 优缺点
    - 资源集中管理，而且降低了耦合度。 
    - IOC容器生成对象是通过Java反射机制，所以在运行效率上有一定损耗。
    - Spring需要大量的配置工作，比较繁琐，所以不适合小项目。

##### AOP


            
### 注解
#### 自动装配
* 组件扫描
    - @Component：表示这个类需在应用程序中被创建
    - @ComponentScan：自动发现应用程序中创建的类 
- 自动装配
    - @Autowired：自动满足bean之间的依赖 
- 定义配置
    - @Configuration：表示当前类是一个配置类
    
#### 自动装配的歧义性
- 首选bean
    - 在声明类的时候使用@Primary
    - 只能定义一个@Primary
- 使用限定符
    - 在声明的时候和装配的时候分别使用@Qualifier
- 使用限定符和bean id
    - 在声明的时候指定bean的id（id即首写字母小写的类名）
    - 在装配的时候使用@Qualifier    
#### Autowired使用场景
- 构造函数
- 成员变量
- setter方法
- 普通方法


### 使用单元测试
AppConfig是测试用新建的Java类。
- AppConfig.java
![AppConfig](https://github.com/mzzzzzzzp/mzzzzzzzp.github.io/blob/master/images/AppConfig.png?raw=true)
- 引入Spring单元测试模块
    - maven：junit、spring-test
    - @RunWith(SpringJUnit4ClassRunner.class)
- 加载配置类
    - @ContextConfiguration(classes=AppConfig.class) 

### log4j
log4j是一个Java编写的、灵活的日志框架，可以快速定位程序出错的位置。
#### 目的
- 监视变量的变化情况，周期性地记录
- 跟踪代码运行时轨迹，日后审计的依据
- 担当集成开发环境中调试器的作用

#### 组成
- logger: 负责捕获、记录日志，可以通过它选择记录不同优先级的日志
- appender: 负责发布日志，可以通过它指定日志的输出位置
- layout: 负责日志的格式，可以通过它按格式输出日志

##### 1.logger
日志优先级顺序为
```
DEBUG < INFO < WARN < ERROR < FATAL
```
其中FATAL为致命错误，会导致程序无法运行；
ERROR为严重错误，主要是程序的错误；
WARN为一般警告，比如session丢失；
INFO为一般要显示的信息，比如登入登出；
DEBUG为程序的调试信息。
##### 2.appender
appender的常用值：
```
1. org.apache.log4j.ConsoleAppender(日志输出到控制台)
2. org.apache.log4j.FileAppender(输出到文件)
3. org.apache.log4j.WriterAppender(将日志以流格式发送到指定地方)
4. org.apache.log4j.DailyRollingFileAppender(每天产生一个日志文件)
```