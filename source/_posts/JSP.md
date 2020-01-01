---
title: JSP
date: 2019-9-23 15:08:22
categories: JSP
---

# JSP

## 概念

Java Server Pages：Java服务器端页面

- 可以理解为一个特殊的页面，既可以指定定义html标签，又可以定义java代码

- 用于简化书写，jsp本质就是一个Servlet类，在service方法中写好了html页面的代码


## 指令

用于配置JSP页面，导入资源文件

```
    <%@ 指令名称 属性名1=属性值1 属性名2=属性值2... %>
```

### 分类
- 1.page：配置JSP页面

        contentType：等同于response.setContentType()
        
            1.设置响应体的mime类型以及字符集
            
            2.设置当前JSP页面的编码
            
        import：导包
        
        errorPage：当前页面发生异常后，自动跳转到指定的错误页面
        
        isErrorPage：标识当前页面是否是错误页面
        
            1.true：是，可以使用内置对象exception打印错误信息到日志中
            
            2.false：默认值，不能打印错误信息
            
- 2.include：页面包含

    可以直接包含其他页面的所有内容

        <%@include file="hello.jsp" %>                        

- 3.taglib: 导入资源，标签库

        <%@ taglib prefix="c" uri="..." %>

## 注释

- 1.HTML注释：
    
    <!--    -->   只能注释HTML代码
    
- 2.JSP注释

    <%--    --%>   可以注释所有代码
    
## JSP的脚本

JSP定义Java代码的方式

- 1.<% 代码 %>：代码其实是在Servlet的service方法中。

- 2.<%! 代码 %>：代码位于成员变量的位置，可能会引发线程安全问题

- 3.<%= 代码 %>：代码会输出到页面上

## JSP的内置对象

即在JSP中不需要获取和创建，可以直接使用的对象

一共有九个对象


| 变量名 | 真实类型 | 作用 |
| :-: | :-: | :-: |
| pageContext | PageContext | 当前页面共享数据，获取其他8个内置对象 |
| request | HttpServletRequest | 一次请求访问多个资源（转发） |
| session | HttpSession | 一次会话的多个请求 |
| application | ServletContext | 所有用户共享数据 |
| response | HttpServletResponse | 响应对象 |
| page | Object | 当前页面（Servlet）的对象 |
| out | JSPWriter | 输出对象 |
| config | ServletConfig | Servlet的配置对象 |
| exception  | Throwable | 异常对象 |


### 对象1.request

### 2.response

### 3.out

out:  字符输出流对象，可以将数据输出到页面上。

#### 特点

和response.getWriter() 类似

    Tomcat给客户端响应前，会先访问response缓冲区数据，再访问out缓冲区数据

    response.getWriter() 输出在 out.Writer() 之前

和<%= 代码 %> 类似 

# MVC开发模式

## 概念

### M：Model，模型。JavaBean实现
    
完成具体的业务操作，如：查询数据库，封装对象
    
### V：View，视图。JSP

展示数据

### C：Controller，控制器。Servlet
1.获取用户的输入
    
2.调用模型
    
3.将数据交给视图展示

## 优缺点

### 优点

- 1.耦合性低，方便维护，利于分工协作

- 2.重用性高

### 缺点

- 使得项目架构变得复杂，对开发人员要求变高


# EL表达式

Expression Language，表达式语言

## 作用
替换和简化jsp页面中的Java代码的编写

## 语法

        ${ 表达式 }
        
## 注释

        1. 设置page指令中：isELIgnored="true"  忽略当前jsp页面中所有的el表达式
        
        2. \${ 表达式 }：忽略当前这个EL表达式
        
## 使用

### 运算
算数运算符：

        + - * /(div) %(mod)
        
比较运算符：

        > < <= >= == !=
        
逻辑运算符：

        &&(and)     ||(or)      !(not)
        
空运算符：

        empty
        
        eg.${empty 键名}、 ${not empty 键名}
        用于判断字符串、集合、数组对象是否为null并且长度是否为0
        
### 获取值

EL表达式只能从域对象中获取值

```
1.${域名称.域名}：从指定域中获取指定键的值

    域名称：
    
        1.pageScope
        2.requestScope
        3.sessionScope
        4.applicationScope
        
        eg. 获取request域中存储的 name = 张三
            ${requestScope.name}

2.${键名}：依次从最小的域中查找是否有该键对应的值，找到为止

3.获取对象、List集合、Map集合：
        
    1.对象：
        
            ${域名称.键名.属性名}
            本质是调用对象的getter方法
            
    2.List集合：
    
            ${域名称.键名[索引]}
            
    3.Map集合：            
                        
            ${域名称.键名.key名称}
            
            ${域名称.键名["key名称"]}            
```

### 隐式对象

pageContext

eg. ${pageContext.request.contextPath}:  动态获取虚拟目录

# JSTL

## 概念

JavaServer Pages Tag Library    JSP标准标签库

- 作用：
    用于简化和替换JSP页面上的Java代码

## 步骤

- 1.导入jstl相关的jar包

- 2.引入标签库
    taglib指令：
        <%@ taglib prefix="c"  uri="  "%>

## 常用的JSTL标签

### if：相当于Java的if语句 

- 属性：
    
    test为必须属性，接收boolean表达式
    
    表达式为true，则执行if标签体内容；一般和El表达式连用
    
        eg.<c:if test=""></c:if>
    
### choose: 相当于Java的switch语句

### foreach：相当于Java的for语句     
                    
        
                                               

