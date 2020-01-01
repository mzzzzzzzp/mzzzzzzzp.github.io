---
title: JSON
date: 2019-9-23 21:24:22
categories: JSON
---

# JSON

## 概念

JavaScript Object Notation  JavaScript对象表示法

        eg. var P = {"name":"张三","age":"23"};


- 多用于存储和交换文本信息的语法

- 进行数据传输

- JSON比XML更小、更快、更易解析

## 语法

### 基本规则

- JSON数据是由键值对构成的，键值对由逗号隔开

- 花括号保存对象：{}
        eg.{"person":{"name":"mzp","age":"20"}}

- 方括号保存数组：[]
        eg.{"persons":[{"":""},{"":""}]}
        
### 获取数据

- JSON对象.键名

- JSON对象["键名"]

- 数组对象[索引]   

## JSON数据和Java对象的相互转换

JSON解析器：jackson...

### JSON转为Java对象

        readValue(json字符串数据，Class)
    
### Java对象转换为JSON     

- 1.    导入jackson的相关jar包

- 2.    创建jackson核心对象 ObjectMapper

- 3.    调用ObjectMapper的相关方法进行转换

        1.转换方法：
        
            writeValue(参数1，obj):
            
                参数1：
                    File：将obj对象转换为JSON字符串，并保存到指定文件中
                    
                    Writer：将JSON数据填充到字符输出流中
                    
                    OutputStream：将JSON数据填充到字节输出流中
                    
            writeValueAsString(obj): 将obj对象转为json字符串
            
        2.注解：
        
            @JsonIgnore：排除属性
            
            @JsonFormat：属性值的格式化
            
                eg. @JsonFormat(pattern="yyyy-MM-dd")
                
        3.复杂Java对象转换
        
            1.List：数组
            
            2.Map：对象格式一致
                                                            