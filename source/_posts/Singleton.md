---
title: Singleton
date: 2019-9-26 19:40:22
categories: Singleton
---

# 单例设计模式

即某个类在整个系统中只能有一个实例对象可被获取和使用的代码模式

eg.     代表JVM运行环境的Runtime类


# 要点

- 该类只能有一个实例

    →   构造器私有化
    
- 必须自行创建这个实例

    →   含有该类的静态变量来保存这个实例
    
- 必须向外部提供这个实例

    →   1.直接暴露
    
    →   2.或者用静态变量的get方法获取
    
    
# 常见形式

## 饿汉式
直接创建对象，不存在线程安全问题

### 直接实例化饿汉式

```
    
/**
 * 构造器私有化
 * 静态变量自行创建
 * final强调这是一个单例
 */
public class Singleton01 {
    public static final Singleton01 Instance = new Singleton01();
    private Singleton01(){

    }
}

```

### 枚举式(最简洁)

```
/**
 * 枚举类型，表示该类型的对象是有限的
 * 限定为一个Instance时，即为单例
 */
public enum Singleton02 {
    Instance
}    

```

### 静态代码块饿汉式

```
import java.io.IOException;
import java.util.Properties;

public class Singleton03 {
    public static final Singleton03 Instance;
    
    //用于复杂情况下初始化
    private String info;
    static{
        Properties pro = new Properties();
        try {
            pro.load(Singleton03.class.getClassLoader().getResourceAsStream("singleton.properties"));

            Instance = new Singleton03(pro.getProperty("info"));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public Singleton03(String info) {
        this.info = info;
    }
}    

```

## 懒汉式      

延迟创建这个实例对象

### 线程不安全（适用于单线程）

```
    

```
### 线程安全（适用于多线程）      

```
    

```

### 静态内部类形式（适用于多线程）

```
    

```