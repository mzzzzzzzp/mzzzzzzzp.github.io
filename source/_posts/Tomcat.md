---
title: Tomcat
date: 2019-8-19 16:31:22
categories: Tomcat
---

# WEB相关知识

## 软件架构

- 1.B/S: 浏览器/服务器端

- 2.C/S：客户端/服务器端

## 资源分类

- 1.静态资源：所有用户访问得到的结果是一样的，静态资源可以直接被浏览器解析。
    eg. HTML、CSS、JavaScript

- 2.动态资源：每个用户访问相同的资源，得到的结果可能不一样。动态资源被访问后，服务器端需要先转换为静态资源，再返回给浏览器。
    eg. servlet/jsp，PHP，asp......
    
    
## 网络通信三要素

- 1.IP
    电子设备在网络中的唯一标识。

- 2.端口
    应用程序在计算机中的唯一标识。 0~~65536

- 3.传输协议            
    规定了数据传输的规则
    基础协议：
            1.tcp： 安全协议，三次握手，四次挥手。 但速度慢
            
            2.udp：不安全协议。速度快

## web服务器软件

服务器：安装了服务器软件的计算机

服务器软件：接受用户请求， 处理请求， 做出响应。

web服务器软件：接受用户请求， 处理请求， 做出响应。
    在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目
    
### 常见Java相关web服务器软件

- webLogic：Oracle公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费。

- webSphere：IBM公司，大型的JavaEE服务器....

- JBOSS: JBOSS公司，大型的JavaEE服务器....

- Tomcat: Apache基金组织，中小型的JavaEE服务器，仅支持少量规范，eg.servlet/jsp，开源免费。

JavaEE：Java语言在企业级开发中使用的技术规范的总和。一共规定了13项大的规范。它们分别是：JDBC、JNDI、EJB、RMI、Servlet、JSP、XML、JMS、Java IDL、JTS、JTA、JavaMail和JAF。    

# Tomcat
web服务器软件

## 下载
[官网地址](http://tomcat.apache.org/)

## 启动

运行 bin/startup.bat

## 访问

http://ip:8080

eg. http://localhost:8080

## 可能遇到的问题

- 1.黑窗口一闪而过：
        没有正确配置JAVA_HOME环境变量
        
- 2.启动报错：
        端口号被占用
        
        一般会将Tomcat的默认端口号改为80。80端口号是HTTP协议的默认端口号，访问时不用输入端口号。        
 
## 关闭

bin/shutdown.bat

ctrl + C

## 配置

### 部署项目的方式

- 1.将项目放在webapps目录下即可

    简化部署：
        将项目压缩为war格式，将war包放到webapps目录下。war包会自动解压缩。
 
- 2.配置conf/server.xml文件
    在<Host>标签体中配置
        <Context docBase="D:\hello" path="/hehe" />
        
        docBase: 项目存放的路径
        path：虚拟目录，即URL上访问的目录
        
- 3.在conf\Catalina\localhost 创建任意名称的xml文件

        <Context docBase="D:\hello" />
        
        虚拟目录：xml文件的名称        

### 动态项目和静态项目

**目录结构**

   java动态项目：
    -- 项目名称
        -- WEB-INF
            -- web.xml: 该项目的核心配置文件
            -- class目录：放置字节码文件
            -- lib目录：放置项目依赖的jar包
    
            