---
title: Servlet
date: 2019-8-19 20:50:22
categories: Servlet
---

# 概念

运行在web服务器端的Java小程序

- Servlet就是一个接口，定义了Java类被浏览器访问（tomcat识别）到的规则

# 快速入门

- 1.创建JavaEE项目

- 2.定义一个类，实现Servlet接口
        public class ServletDemo01 implements Servlet{
       
        }

- 3.实现接口中的抽象方法

- 4.配置Servlet

    在web.xml中配置：
               
        <servlet>
            
            <servlet-name>demo</servlet-name>
            <servlet-class>ServletDemo01 的全类名</servlet-class>
            
        </servlet>
        
        <servlet-mapping>
        
            <servlet-name>demo<servlet-name>
            <url-pattern>/demo</url-pattern>                
        
        </servletmapping>
        
# 执行原理

- 1.当服务器接收到客户端浏览器的请求后，会解析请求URL路径，获取访问的Servlet资源路径

- 2.查找web.xml文件，是否有对应的<url-pattern>标签体内容

- 3.有相同的就根据<servlet-name>再去查找 <servlet-class> 全类名

- 4.tomcat会将字节码文件加载进内存，并创建对象

- 5.调用其方法

# Servlet中方法的生命周期

- 1.被创建：执行init方法，只执行一次
    
    Servlet创建时间：
            
        默认情况下，第一次被访问时会创建。
        
        在<servlet>标签下配置：
            
            1.第一被访问时创建
                
                <load-on-startup>的值为负数
                
            2.在服务器启动时创建
                
                <load-on-startup>的值为0或正整数 
                
    init方法只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例的
        多个用户同时访问时，存在线程安全问题；
    解决方法：    
        尽量不要在Servlet中定义局部变量；或者不要对局部变量进行修改操作。
        
- 2.提供服务：执行service方法，执行多次
    
    每次访问Servlet，service方法都会被调用一次
    
- 3.被销毁：执行destroy方法，只执行一次

    Servlet被销毁时执行。服务器关闭时，Servlet被销毁。
    用于释放资源。
    
    
# 注解配置Servlet

- 1.创建JavaEE项目，不用创建web.xml

- 2.定义一个类，实现Servlet接口

- 3.复写方法

- 4.在类上使用@WebServlet注解，进行配置：
        eg. @WebServlet("资源路径(eg. /demo01)")
        
# IDEA与Tomcat的相关配置

- 1.IDEA会为每一个tomcat部署的项目单独建立一份配置文件
    
    查看控制台的log: Using CATALINA_BASE: "......"
    
- 2.工作空间项目    和  tomcat部署的项目

    tomcat真正访问的是 "tomcat部署的项目"， 部署的项目对应“工作空间项目”的web目录下的所有资源
    
    WEB-INF目录下的资源不能被浏览器直接访问。
    
    
# Servlet的体系结构

## Servlet 接口

## GenericServlet 抽象类

将Servlet接口中其他的方法都做了默认空实现，只将service()方法作为抽象。

定义Servlet时，只需要实现 service() 方法即可。

## HttpServlet 抽象类

对HTTP协议的一种封装，简化操作

方法：    
   
   1.定义类继承HTTPServlet
   2.复写doGet/doPost方法
   
## Servlet相关配置

url-pattern：Servlet访问路径
    
   1. 一个Servlet可以定义多个访问路径：
        
            @WebServlet({"/demo1","/demo2","/demo3"})
        
   2.路径定义规则：
   
    1./xxx ：路径匹配
    
    2./xxx/xxx: 多层路径，目录结构
    
    3.*.do: 扩展名匹配          
                                                                       