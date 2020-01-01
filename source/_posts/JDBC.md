---
title: JDBC
date: 2019-8-9 15:02:22
categories: JDBC
---

### 概念
Java Databases Connectivity,Java数据库连接。
- 本质：
    其实是sun公司定义的一套操作所有关系型数据库的规则，即接口。
    各个数据库厂商实现这套接口，提供数据库驱动jar包。
    我们可以使用这套接口（JDBC）编程，真正执行的是驱动jar包中的实现类。
    
### 步骤
#### 1.导入驱动jar包
            jar 复制到项目libs目录下，右键libs-->add as library;
            
#### 2.注册驱动
        Class.forName("com.mysql.jdbc.Driver");            
#### 3.获取数据库连接对象Connection            
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/db3","root","root");
#### 4.定义SQL语句
        String sql = "update account set balance = 500 where id = 1";            
#### 5.获取执行SQL的对象Statement            
        Statement stmt = conn.createStatement();
#### 6.执行SQL，接受返回结果            
        int count = stmt.executeUpdate(sql);
#### 7.处理结果            
        System.out.println(count);
#### 8.释放资源
        stmt.close();
        conn.close();
        (补充)rs.close();

### 步骤里面的各个对象
- 1.DriverManager: 驱动管理对象
- 2.Connection：数据库连接对象
        1.获取执行sql的对象
            Statement createStatement()
            PreparedStatement prepareStatement(String sql)
            
        2.管理事务：
            - 开启事务：setAutoCommit(boolean autoCommit):调用该方法，并入参为false，即开启事务；
            - 提交事务：commit();
            - 回滚事务：rollback();            

- 3.Statement：执行静态sql对象
        int executeUpdate(String sql):
            执行DML(insert、update、delete)语句、DDL(create、alter、drop)语句；
            
        ResultSet executeQuery(String sql):
            执行DQL(select)语句            
- 4.ResultSet：结果集对象
        boolean next():游标向下移动一行
        getXX(): 获取数据。参数为该列列名
        eg.
            getInt()、getString()
        ResultSet rs 结束后也需要释放资源。
        
- 5.PreparedStatement：执行（动态）预编译sql对象     
可以防止SQL注入；
执行效率更高。
  - 1.SQL注入问题：在拼接SQL时，有一些SQL的特殊关键字参与字符串的拼接，会造成安全性问题。
        
  - 2.解决SQL注入的问题：使用PreparedStatement对象来解决；
  - 3.预编译SQL：参数使用?作为占位符；
        
  - 4.步骤：
            导入驱动jar包;
            ......
            定义SQL，参数使用占位符：select * from user where username = ? and password=?;
            获取执行SQL语句的对象：PreparedStatement Connection.prepareStatement(String sql);
            --给?赋值-- ：setXXX(?的位置从1开始,？的值);
            执行SQL语句，不需要传递SQL；
            ......
            
### 数据库连接池
#### 概念
是一个容器（集合），用于存放数据库连接的容器。
系统初始化后，容器被创建，容器会申请一些连接对象，当用户访问数据库时，从容器中获取连接对象，用户访问完之后，会将连接对象归还给容器。
#### 实现
- Java定义了标准接口：DataSource  javax.sql包下面
   方法：
        获取连接：
            getConnection()
        归还连接：
            Connection.close()
- Java只是提供了接口，由数据库厂商实现连接池技术
    1.C3P0
    2.Druid                       

##### C3P0
###### 1.导入jar包
        c3p0-0.9.5.2.jar 
        mchange-commons-java-0.2.12.jar
        mysql-connection-java-5.1.37-bin.jar     

###### 2.定义配置文件
   名称：c3p0.properties 或者 c3p0-config.xml
   路径：将配置文件放在src目录下。
   
###### 3.创建核心对象  数据库连接池对象
    DataSource ds = new ComboPooledDataSource();
    
###### 4.获取连接
    Connection conn = ds.getConnection(); 
    
##### Druid
###### 1.导入jar包
        druid-1.0.9.jar
        
###### 2.定义和加载配置文件
    properties形式的，可以放在任意目录下面
    加载配置文件：（DruidDemo为类名）
    Properties pro = new Properties();
    InputStream is = DruidDemo.class.getClassLoader().getResourceAsStream(配置文件名称.properties);
    pro.load(is);
###### 3.获取数据库连接池对象
    通过工厂类来获取：
        DataSource ds = DruidDataSourceFactory.createDataSource(pro);
###### 4.获取连接
    Connection conn = ds.getConnection();
    
### Spring JDBC
Spring框架对JDBC的简单封装，提供了一个JDBCTemplate对象简化JDBC的开发
#### 步骤
##### 1.导入jar包
        Spring的jar包
        mysql的jar包
        数据库连接池的jar包
##### 2.创建JDBCTemplate对象，依赖于数据源DataSource。
        JdbcTemplate template = new JdbcTemplate(ds); //ds为上文获取到的数据库连接池对象

##### 3.调用JDBCTemplate的方法来完成CRUD操作
                   
        update(): 执行DML语句，增、删、改语句；
        queryForMap(): 将查询结果封装为Map集合；
            该方法查询结果集长度为1；
                                                     
        queryForList(): 将查询结果封装为List集合；
            将每一条记录封装为一个Map集合，再将Map集合装载到List集合中；
        
        query(): 查询结果封装为JavaBean对象；
            new BeanPropertyRowMapper<类型>(类型.class)
            可以实现数据到JavaBean的自动封装；
        queryForObject：查询结果封装为对象。 
            一般用于聚合函数的查询。                                        