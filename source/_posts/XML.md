---
title: XML
date: 2019-8-18 17:02:22
categories: XML
---

# 概念

Extensible Markup Language, 可扩展标记语言

可扩展，即标签都是自定义的。

## 功能

### 存储数据
- 1.配置文件
- 2.在网络中传输

## XML和HTML的区别

- 1.XML标签都是自定义的，HTMl标签是预定义的；
- 2.XML语法严格，HTML语法松散；
- 3.XML是存储数据的，HTML是展示数据的。

# 语法

## 基本语法

- 1. XML文档的后缀名为  .xml
- 2. XML第一行必须定义为文档声明，eg.  <?xml version='1.0' ?>
- 3. XML文档中有且仅有一个根标签
- 4. 属性值必须用引号引起来
- 5. 标签必须正确关闭
- 6. 标签区分大小写

## 入门示例
        
```
    <?xml version = '1.0' ?>
    <users>
        <user id = '1'>
            <name>xiaoming</name>
            <age>18</age>
            <br/>
        </user>
        <user id = '2'>
            <name>xiaohong</name>
            <age>18</age>
            <br/>
        </user>
    </users>
    
```        

## 组成部分

### 文档声明

- 1.格式
        <?xml 属性列表 ?>

- 2.属性列表
        version：版本号，必须具有的属性
        
        encodeing：编码方式。告知解析引擎当前文档使用的字符集
        
        standalone：是否独立
        
### 指令（了解）：结合CSS

```markdown
    <?xml-stylesheet type="text/css" href="" ?>
```        

### 文本
   CDATA区：在该区域中的数据会被原样展示
        格式：<![CDATA[数据]]]>

## 约束

规定XML文档的书写规则

### 分类

- DTD：一种简单的约束技术
- Schema：复杂的约束技术

#### DTD
引入DTD文档到XML文档中
   - 1.内部DTD：将约束规则定义在XML中
   - 2.外部DTD：将约束规则定义在外部DTD文件中
         外部DTD：
            本地：<!DOCTYPE  根标签名 SYSTEM "DTD文件的位置">
            网络：<!DOCTYPE  根标签名 SYSTEM "DTD文件名字" "DTD文件的位置URL">
 
#### Schema

引入：
    1.填写XML文档的根元素
    2.引入xsi前缀    xmlns:xsi=""http://www.w3c.org/2001/XMLSchema-instance"
    3.引入xsd文件命名空间  xsi:schemaLocation=""http://www......"  student.xsd
    4.为每一个xsd约束声明一个前缀，作为标识  xmlns=""http://www...."
    
# 解析

操作XML文档，将文档中的数据读取到内存中；

## 操作XML文档

- 1.解析（读取）：将文档中的数据读取到内存中

- 2.写入：将内存中数据保存到XML文档中，持久化存储。

## 解析XML方式

- 1.DOM：将标记语言文档一次性加载到内存中，在内存中形成一棵DOM树。
    
    优点：操作方便，可以对文档进行CRUD操作
    缺点：占内存
    
- 2.SAX：逐行读取，基于事件驱动。    
     
     优点：不占内存
     缺点：逐行读取，不能增删改操作
     
## 常见的XML解析器

- 1.JAXP     
- 2.DOM4J     
- 3.Jsoup    
   是一款Java的HTML解析器，可直接解析某个URL地址、HTML文本内容。
    
- 4.PULL 
    Android操作系统内置的解析器，SAX方式的。
    
### Jsoup

#### 快速入门

- 1.导入jar包
- 2.获取Document对象
- 3.获取对应的标签Element对象
- 4.获取数据

```markdown

    1.获取student.xml的path
    String path = JsoupDemo01.class.getClassLoader().getResource("student.xml").getPath();
    
    2.解析xml文档，加载文档进内存，获取DOM树(Document)
    Document document = Jsoup.parse(new File(path),"utf-8");
    
    3.获取元素对象Element
    Elements elements = document.getElementsByTag("name");
    
    3.1 获取第一个name的Element对象
    Element element = element.get(0);
    
    3.2 获取数据
    String name = element.text();
```       

#### 对象

- 1.Jsoup：工具类，可以解析HTML或XML文档，返回Document
        parse：解析HTML或XML文档，返回Document
        
- 2.Document：文档对象。代表内存中的dom树
        获取Element对象
            getElementById()
            ......
            
- 3.Elements：元素Element对象的集合。可以当做ArrayList<Element>来使用

- 4.Element：元素对象
    1.获取子元素对象
    2.获取属性值
        String attr(String key)：根据属性名称获取属性值
        
    3.获取文本内容
        String text()：获取文本内容
        String html(): 获取标签体的所有内容（包括字标签的字符串内容）
        
- 5.Node：节点对象
    是Document和Element的父类        
                                 
                                 
#### 快捷查询

- 1.selector：选择器
    使用方法：Elements select(String cssQuery)

- 2.XPath: XPath即为XML路径语言，用来确定XML文档中某部分位置的语言
    
    使用Jsoup的XPath时需要额外导入jar包；
    查询W3C参考手册。                                                
            