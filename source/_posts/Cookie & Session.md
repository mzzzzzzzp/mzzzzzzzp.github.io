---
title: Cookie & Session
date: 2019-9-22 16:05:22
categories: Cookie & Session
---

# 会话技术

## 概念

一次会话中包含多次请求和响应

- 一次会话：浏览器第一次给服务器资源发送请求，会话建立，直到有一方断开为止。

## 功能

在一次会话的范围内的多次请求间，可以共享数据

## 方式

- 客户端会话技术：Cookie

- 服务器端会话技术：Session

# Cookie

## 概念
客户端会话技术，将数据保存到客户端中  

## 快速入门

- 1.创建Cookie对象，绑定数据
            
            new Cookie(String name,String value);
    
- 2.发送Cookie对象
        
            response.addCookie(Cookie cookie)
            
- 3.获取Cookie，拿到数据

            Cookie[] request.getCookies()


### 演示

ServletCookie

```markdown
package cn.whu.web.Cookie;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/ServletCookie")
public class ServletCookie extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.创建Cookie
        Cookie c1 = new Cookie("mzp","male");
        Cookie c2 = new Cookie("mzp","male");
        Cookie c3 = new Cookie("mzp","male");

        //2.发送Cookie
        response.addCookie(c1);
        response.addCookie(c2);
        response.addCookie(c3);
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }
}


```

ServletCookie02

```markdown
package cn.whu.web.Cookie;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/ServletCookie02")
public class ServletCookie02 extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 1.获取Cookie
        Cookie[] cookies = request.getCookies();

        //2.打印Cookie
        //2.1设置响应消息体的数据格式以及编码
        response.setContentType("text/html;charset=utf-8");
        for (Cookie cookie : cookies) {
            String name = cookie.getName();
            String value = cookie.getValue();
            response.getWriter().write(name);
            response.getWriter().write(value);
            System.out.println( name +":" + value);
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request,response);
    }
}

```    

## 实现原理

基于响应头set-cookie  将cookie发送到浏览器端

基于请求头cookie   将cookie发送给服务器端

## Cookie细节

### 1.一次能否发送多个Cookie？

可以创建多个Cookie对象，多次调用response对象的addCookie方法即可

### 2.Cookie在浏览器中保存多长时间？

- 1. 默认情况，浏览器关闭后，Cookie数据即被销毁

- 2. 持久化存储
```markdown

setMaxAge(int seconds)

    1.seconds 为正数：将Cookie写入硬盘持久化存储，保留至seconds时间后销毁
    
    2.0：删除Cookie信息
    
    3.负数：默认值，即随浏览器关闭销毁
```
        
- 4.Cookie共享问题？

1.同一个Tomcat服务器中，部署了多个web项目，项目之间Cookie不能共享

    setPath（String path）  将path设置为 "/" 后，项目之间可以共享。
    
2.不同Tomcat服务器间Cookie不能共享

    setDomain(String path)  设置一级域名相同，多个服务器之间可以共享
        eg. setDomain(baidu.com)，那么  tiba.baidu.com 和   news.baidu.com  中的Cookie可以共享
        

## Cookie的特点和作用

### 特点：

- 1.Cookie存储数据在客户端浏览器

- 2.浏览器对于单个cookie的大小有限制（4kb） 以及对于同一个域名下的总cookie数量也有限制（20个）

### 作用：

- 1.cookie一般用于存储少量不太敏感的数据

- 2.在不登录的前提下，完成服务器对客户端的身份识别



# Session
## 1. 概念
服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端的对象中

## 2. 快速入门

- 1.获取HttpSession对象：

        HttpSession session = request.getSession();

- 2.HttpSession对象：

        Object getAttribute(String name)
        
        void setAttribute(String name)
        
        void removeAttribute(String name)
    
## 3. 原理

Session的实现是依赖于Cookie的：

- 1.第一次getSession时，若没有Session，则会创建一个Session对象，

- 2.并且将该对象的 "id=XXXXXX" 属性以Cookie的方式传递给浏览器

- 3.浏览器再次发起请求时，会在请求头中发送这个Cookie

## 4. 细节

### 1. 客户端关闭。服务器不关闭，前后获取的Session不是同一个

如果需要相同，则可以创建Cookie，键为 JSESSIONID，设置最大存活时间，让Cookie持久化保存
        
        Cookie cookie = new Cookie("JSESSIONID",session.getID());
        
        cookie.setMaxAge(60*60);  //60*60 = 一小时
        
        response.addCookie(cookie);
        
### 2. 客户端不关闭，服务器关闭后，如何确保获取相同的Session信息？

Tomcat服务器实现了自动Session钝化和活化，在work目录中生成了Session的序列化文件。

- 1. Session钝化

    在服务器正常关闭之前，将Session对象序列化到硬盘上，持久化存储

- 2. Session活化          

    服务器启动后，将Session文件转化为内存中的Session对象即可
    
### 3. Session什么时候被销毁？

- 1.服务器关闭

- 2.Session对象调用invalidate()

- 3.Session默认失效时间为  30分钟

在tomcat的web.xml 中设置

    <session-config>
            
        <session-timeout>30</session-timeout>            
        
    </session-config>    

## 5.特点

- 1.Session用于存储一次会话的多次请求数据，存储在服务器端

- 2.Session可以存储任意类型和大小的数据

## 6.Session和Cookie的区别

- 1.Session存储数据在服务器端，Cookie存储在客户端

- 2.Session没有数据大小限制，Cookie有

- 3.Session数据安全，Cookie相对于不安全
          
        