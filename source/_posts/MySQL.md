---
title: MySQL学习笔记
date: 2019-4-28 11:53:22
categories: MySQL
---
### 数据库原理
**Database(DB)**
数据库是保存有组织数据的容器。
数据库系统的组成：
1. 数据库
    - 存放数据的仓库，按一定的格式储存
2. 数据库管理系统
    - 建立、管理、维护数据库的系统软件
3. 数据库应用系统
    - 使用到数据库技术的应用软件
    
### 数据库特点

- 1.持久化存储数据，本质上是一个文件系统。
- 2.方便存储和管理数据。
- 3.使用统一的方式操作数据库(SQL)。    
    
### MySQL简介
MySQL是一个RDBMS(Relational Database Management System,关系型数据库管理系统)，是WEB应用中最好的数据库管理系统。关系型数据库将数据保存在不同的表中，而非置于一个大仓库中，因此提高了速度和灵活性。

#### 开启和关闭服务
管理员打开cmd
- net start mysql
- net stop mysql

#### 登录
- 1.mysql -uroot -proot;
- 2.mysql -hip(ip地址) -uroot -proot
- 3.mysql --host=ip --user=root --password=root

#### 退出
- 1.exit 
- 2.quit 

### SQL
Structured Query Language,结构化查询语言。它定义了操作所有关系型数据库的规则。

#### 分类

- 1.**DDL**(Data Definition Language)数据定义语言：用来定义数据库、表、列等，关键字：create、drop、alter等；
- 2.**DML**(Data Manipulation Language)数据操作语言：用来对表中的数据进行增删改，关键字：insert、delete、update。
- 3.**DQL**(Data Query Language)数据查询语言：用来查询表中的数据，关键字：select、where。
- 2.**DCL**(Data Control Language)数据控制语言：用来定义数据库的访问权限及创建用户，关键字：grant、revoke。

#### CRUD
##### 数据库的操作(DDL)

- 1.C(Create): 创建
        - 创建数据库：
        create database 数据库名称；
        - 创建数据库前判断是否存在：
        create database if not exists 数据库名称；
        - 创建数据库并指定字符集：
        create database 数据库名称 character set 字符集名；
        
- 2.R(Retrieve): 查询
        - 查询所有数据库名称：
        show databases;
        - 查询某个数据库的创建语句：
        show create database 数据库名称;         

- 3.U(Update): 修改
        - 修改数据库的字符集：
        alter database 数据库名称 character set 字符集名称；
- 4.D(Delete): 删除
        - 删除数据库：
        drop database 数据库名称；
        
- 5.使用数据库
        - 查询当前使用的数据库：
        select database();
        - 使用数据库：
        use 数据库名称；        

##### 表的操作(DDL)

- 1.C(Create): 创建
        - create table 表名(
            列名1 数据类型1，
            列名2 数据类型2，
            列名3 数据类型3，
            列名n 数据类型n
        );
        *注意*：最后一列，不加逗号。
                    
- 2.R(Retrieve): 查询
        - 查询某个数据库的所有表：
        show tables;
        - 查询表结构：
        desc 表名;

- 3.U(Update): 修改
        - 修改表名：
        alter table 表名 rename to 新的表名;
        - 修改字符集:
        alter table 表名 character set 字符集名称;
        - 添加一列：
        alter table 表名 add 列名 数据类型;
        - 修改列名称 类型
        alter table 表名 change 列名 新列名 数据类型;
        alter table 表名 change 列名 新数据类型;
        - 删除列
        alter table 表名 drop 列名；

- 4.D(Delete): 删除
        - drop table 表名;
        - drop table if exists 表名;
        
        
##### 对记录的操作(DML)  

- 1.添加数据：
        - insert into 表名(列名1，列名2...) values(值1，值2...);
        *注意*：
            1.表名后面不定义列名，则默认给所有列添加值；
            2.除了数字类型，其他类型数据需要使用引号。
            
- 2.删除     
        - delete from 表名 where 条件;
        *注意*：
            1.如果不添加条件，则删除表中所有记录，但执行效率慢；
            2.删除所有记录： truncate table 表名;  执行效率高
            
- 3.修改数据
        - update 表名 set 列名1=值1，列名2=值2  where 条件;
        *注意*：
            如果不添加条件，会修改表中所有记录。
        
##### 查询表中的记录(DQL)
- select * from 表名;
- 1.*语法*：
        select  字段列表
        from    表名列表
        where   条件列表
        group by    分组字段
        having  分组之后的条件
        order by    排序
        limit   分页限定
        
- 2.*基础查询*：
    1.多个字段查询
        select 字段名1,字段名2  from 表名;
    2.去除重复
        distinct
    3.计算列
        可以使用四则运算；
        ifnull(表达式1，表达式2)
            *表达式1：需要判断是否为null的字段；
            *表达式2：如果为null的替换值；                                             
    4.起别名
        as(as可以省略)
        
- 3.*条件查询*：
    where子句后跟条件
    运算符：
        >、<、<=、>=、=、<>、!=
        between...and
        in(集合)
        like:模糊查询
            _:单个任意字符
            %:多个任意字符
        is null
        and/&&
        or/||
        not/!    
        
- 4.*排序查询*：
        order by 排序字段1 排序方式1，排序字段2 排序方式2...
        - asc: 升序，默认为asc；
        - desc: 降序；
        如果有多个排序条件，当前边的条件值一样时，才会判断第二条件。
        
- 5.*聚合函数*：将一列数据作为一个整体，进行*纵向*计算。
        - count、max、min、sum、avg
        eg. select count(id) from myTable;                   
- 6.*分组查询*：   
        - group by 分组字段;
        - where: 在分组之前进行限定，如果不满足条件，则不参与分组；不可以跟聚合函数。
        - having：在分组之后进行限定，不满足结果就不会被查询出来；可以进行聚合函数的判断。
                          
- 7.*分页查询*：                    
        - limit 开始的记录的索引，每页查询的条数；
        - 开始的索引 = （当前的页码 - 1）* 每页显示的条数；
        - limit是一个MySQL的“方言”；
        
### 表的约束
对表中的数据进行限定，保证数据的正确性、有效性和完整性。
#### 非空约束（值不能为null）：not null
```markdown
eg.创建表时添加非空约束：
    create table stu(
        id int,
        name varchar(20) not null
    );
   删除约束：
    alter table stu modify name varchar(20);
   给创建的表添加非空约束：
   alter table stu modify name  varchar(20) not null; 
   
```

#### 唯一约束（值不能重复）：unique
```markdown
eg.创建表时添加唯一约束：
    create table stu(
        id int,
        name varchar(20) unique
    );
    删除唯一约束：
    alter table stu drop **index** name;
```
#### 主键约束（记录的唯一标识）：primary key
```markdown
eg.创建表时添加主键约束：
    create table stu(
        id int primary key,
        name varchar(20) 
    );
    删除主键约束：
    alter table stu drop **primary key**;

    添加自动增长：
    alter table stu modify id int auto_increment,


```

#### 外键约束（表与表之间产生关系）：foreign key
```markdown
    1.创建表时，添加外键：
    create table stu(
        id int,
        外键列,
        constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
    );
    
    2.删除外键：
    alter table stu drop foreign key 外键名称;
    
    3.创建表后，添加外键：
    alter table stu add constraint 外键名称 foreign key (外键列名称);
    
    4.级联操作
    级联更新：
    alter table stu add constraint 外键名称 foreign key （外键列名称）references 主表名称(主表列名称) on update cascade;
    级联删除：
    alter table stu add constraint 外键名称 foreign key （外键列名称）references 主表名称(主表列名称) on delete cascade;
```
     
### 数据库的设计

#### 多表之间的关系
##### 分类
- 一对一
    eg. 人和身份证
- 一对多
    eg. 员工和部门
        - 实现方式：在多的一方建立外键，指向另一个表的主键。
- 多对多
    eg. 学生和课程
        - 实现方式：借助第三张中间表，中间表包含两个字段，分别指向两张表的主键。

#### 数据库范式
设计数据库时，需要遵循的一些规范。遵循后面的范式，必须遵循前面的所有范式。
##### 第一范式(1NF)
每一列都是不可分割的原子数据项。
##### 第二范式(2NF)
在1NF的基础上，非码属性必须完全依赖于码（**在1NF基础上消除非主属性对主码的部分函数依赖**）。
    - 函数依赖：通过A属性（属性组）的值，可以确定唯一B属性的值，则称B依赖于A。
    - 完全函数依赖、部分函数依赖、传递函数依赖。
    - 码：表中，一个属性或属性组，被其他所有属性完全依赖，这个属性（属性组）为该表的码。
    - 主属性：码属性组中的所有属性。
##### 第三范式(3NF)
在2NF的基础上，任何非主属性不依赖于其它非主属性（**在2NF基础上消除传递依赖**）。


### 数据库备份和还原

#### 命令行
##### 备份
        - mysqldump -u用户名 -p密码 数据库名称 > 保存的路径;
##### 还原
        - 1.创建数据库；
        - 2.使用数据库；
        - 3. source 文件路径;
        
### 多表查询
```
select * from 表1的名称，表2的名称;
```

#### 分类
##### 内连接查询
- 隐式内连接：使用where条件消除无用数据；
 ```markdown
      select * from 表1名称，表2名称 where 条件;
 ```
- 显式内连接：
```markdown
      select * from 表1名称 inner join 表2名称 on 条件;
```

##### 外连接查询
- 左外连接：
    查询左表所有数据以及两个表的交集部分；
```markdown
    select 字段列表 from 表1 left outer join 表2 on 条件；    
```
- 右外连接
    left替换为right。
    
    
### 事务
#### 基本介绍
##### 概念
如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
##### 操作
- 开启事务：
        start transaction;
        
- 回滚：
        rollback;
- 提交：
        commit;
                
##### 四大特征
- 1.原子性：
    是不可分割的最小操作单位，同时成功或者同时失败。
    
- 2.持久性：
    当事务提交或回滚后，数据库会持久化的保存数据。
            
- 3.隔离性：
    多个事务之间相互独立。            
- 4.一致性：            
    事务操作前后，数据总量不变。
    
##### 事务的隔离级别
多个事务操作同一批数据，会引发问题，设置不同的隔离级别可以解决问题。
- 1.脏读：一个事务，读取到另一个事务没有提交的数据；
- 2.不可重复读（虚读）：在同一个事务中，两次读取到的数据不一样；
- 3.幻读：一个事务操作（DML）数据表中所有记录，另一事务添加了一条数据，则第一个事务查询不到自己的修改。

**分类**：
            - 1.read uncommitted：读未提取
                产生的问题：脏读、不可重复读、幻读
            2.read committed：读已提取（Oracle默认）
                产生的问题：不可重复读、幻读
            3.repeatable read：可重复读（MySQL默认）
                产生的问题：幻读
            4.serializable：串行化
                可以解决所有问题。
                
            1->4，安全性变高，但效率降低 
               
               
### DCL
#### 管理用户
##### 添加用户
        create user "用户名" @"主机名" identified by "密码";
##### 删除用户
        drop user "用户名" @"主机名";
##### 修改用户密码
        update user set password=password("新密码") where user="用户名";
        
        忘记密码：
        1. cmd(管理员运行): net stop mysql;
        2. mysqld --skip-grant-tables;(使用无验证方式启动mysql服务)
        3. 打开新的cmd：mysql;
        4. 设置新密码;
        5. 关闭窗口；
        6. 任务管理器关闭mysqld.exe 进程；
        7. 启动mysql服务：net start mysql;

##### 查询用户
        use mysql;
        select * from user;
               
#### 权限管理
##### 查询权限
        show grants for "用户名"@"主机名";
        eg.:
            show grants for "mzp"@"%";
##### 授予权限
        grant 权限列表 on 数据库名.表名 to "用户名"@"主机名";
        
        eg.
        grant all on *.* to "mzp"@"localhost";
##### 撤销权限
        revoke 权限列表 on 数据库名.表名 from "用户名"@"主机名";                    
                    
### 数据库常用命令


db_name为数据库名称，数据库的命令和表的操作命令类似，将database替换为table。
#### 新建数据库
```
create database db_name;
```
#### 显示已有数据库
```
show database;
```
#### 删除已有数据库
```
drop database db_name;
```
#### 选择数据库
```
use db_name;
```
#### 查看正在使用的数据库
```
select database();
```
#### 创建数据表
**varchar**
- 一种可变长度的类型，varchar(32)指32个字符，可存放32个数字、字母或汉字。 
- 在进行检索时，如果列值的尾部有空格，char列会删除空格，varchar则会保留空格。
- 对于MyISAM表，推荐使用char类型；对于InnoDB表，推荐使用varchar类型。

```
create table tab_name(
id int primary key auto_increment,
username varchar(32),
password varchar(32),
);
```

### 针对数据表的增删改查命令
tab_name为操作的表名，values里面是增加的数据。
#### 增加数据
```
insert into tab_name values(....);
```
#### 删除数据
```
delete from tab_name where 条件;    
```
#### 修改数据
```
update tab_name set name=newname where 条件;    
```
#### 查询数据
```
select * from tab_name;
```
