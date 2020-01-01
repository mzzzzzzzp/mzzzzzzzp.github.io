---
title: Redis
date: 2019-7-24 15:02:22
categories: Redis
---
# 简介
- Redis是C语言开发的开源免费的高性能Key-Value数据库。

- NOSQL(Not Only SQL)系列的非关系型数据库，数据缓存在内存中

- 通常被称为数据结构服务器，因为value可以是String、Hash、List、Set、SortedSet等类型。

# 特点

- 支持数据的持久化，即可以将内存中的数据保存在磁盘中，重启时再次加载使用。

- 不仅支持key-value类型的数据，还提供list，set，hash等数据结构的存储。


# 文件说明

```
    redis.windows.conf   配置文件
    
    redis-cli.exe       Redis的客户端
    
    redis-server        Redis的服务器端
```

# 命令操作

## 数据结构

redis存储的是key，value格式的数据 ，其中key都是字符串，value有5种不同的数据结构


```
    value的数据结构：
    
        1.String
        
        2.Hash：Map格式
        
        3.列表类型 list：LinkedList格式，支持重复元素
        
        4.集合类型 set：不允许重复元素
        
        5.有序集合类型 SortedSet：不允许重复，且元素有序
    
```

## 字符串类型操作 String

- 存储：

        set key value
        
        eg.    set name mzp
        
- 获取：

        get key
        
        eg.     get name

- 删除：

        del key
        
        eg.     del name

## 哈希类型 Hash

- 存储：

        hset key field value
        
        eg.     hset myHash name mzp
        
- 获取：

        1.  hget key field: 获取指定field的值
        
        eg.     hget myHash name
        
        2.  hgetall key:  获取所有的field和value
        
        eg.     hgetall myHash
        
- 删除:

        hdel key field
        
        eg.     hdel myHash name
        
        
## 列表类型  List

简单的字符串列表，按照插入顺序排序。

可以添加元素到列表的左边或者右边

- 存储：
        
        1.  lpush key value:  从左边存入列表
        
        2.  rpush key value：  从右边存入列表
        
- 获取：
        
        lrange key start end    范围获取

- 删除:

        lpop key:  从列表的最左边移除一个元素，并将元素返回
        
        rpop key： 从列表的最右边移除一个元素并返回
        
## 集合类型  set

不允许存储重复的元素

- 存储：

        sadd key value
        
- 获取

        smembers key    获取set集合中所有的元素
                
- 删除                

        srem key value  删除set集合中的某个元素
        
## 有序集合类型 SortedSet

利用score来排序

可以制作实时排行热搜榜。

- 存储
        zadd key score value
        
- 获取        
        1. zrange key start end
        
        2. zrange key start end withscores  获取key和value
        
        zrange key 0 -1  获取所有元素

- 删除        
        zrem key value

## 通用命令

```
    keys * :    查询所有的键
    
    type key：   获取键对应的value的类型
    
    del key：    删除指定的key value
```    
            
# 持久化

Redis是一个内存数据库，Redis服务器重启后数据就会丢失，可以将Redis内存中的数据持久化保存到硬盘文件中。

## RDB 

默认方式，不需要配置

redis.windows.conf 配置文件里面save 100 3  ，表示100秒之后有3次键改变就持久化一次

## AOF

日志记录的方式，可以记录每一条命令的操作

redis.windows.conf 配置文件里面的 appendonly no（关闭AOF）

# Java客户端  Jedis

Java操作redis数据库的工具类

## 步骤

- 1. 下载jedis的jar包

- 2.使用

        //1.获取连接
        
        Jedis jedis = new Jedis("Localhost",6379)                        
        
        //2.操作
        
        jedis.set("username","zhangsan");
                                
        //3.关闭连接                        
        
        jedis.close();
                