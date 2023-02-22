---
title: 深入理解框架之 —— mybatis
img: 'http://pic.tanzhang.work/blog/gallary/230221.png!up.webp'
top: false
cover: 'http://pic.tanzhang.work/blog/gallary/230221.png!up.webp'
toc: true
categories: 框架
tags:
  - mybatis
abbrlink: a21a4e35
date: 2023-02-21 21:24:36
coverImg:
---
## 1. 初识mybatis框架

ORM（全称 Object Relation Mapping） 框架翻译过来就是指对象 - 关系映射框架，故名思意，就是完成对象到关系型数据库之间的映射关系的框架。通过将关系型数据库包装成对象模型的形式，程序可以不再直接去访问底层的数据库，而是以操作对象的方式来完成持久化操作，对于基于面向对象设计的语言是一种极大的便利。

mybatis 就是一款 ORM 的半自动轻量级的持久化框架，之所以说它是半自动的，是因为使用它以后，sql依然需要自己手动编写，但关于数据源的管理，以及参数设置，结果封装等其他事情，都可以放心的交给它来完成。

半自动的框架的优势在于，它可以很方便的去定制sql语句，这对于熟悉sql语言的程序员来说是一种极大的便利，可以很方便的去完成 sql 语句优化。另外，mybatis 将 sql 语句编写在配置文件中，和代码分离开来，可以很方便的完成对 sql 的管理；

当然，半自动也会带来一些问题，由于使用的都是数据库原生的 sql 语句，所以当切换不同类型的数据库时，如果数据库使用的 sql 语法有一定差异，就不可避免的会带来一些兼容性问题，这一点在更换数据库的时候要格外注意。

## 2. mybatis 配置文件深入

mybatis 将配置文件分为两种，第一种是 SqlMapConfig.xml，这是 mybatis 的核心配置文件，用于存储 数据源 等信息。第二种是 Mapper.xml，这种配置文件主要用于存储自定义的 sql 语句。

### 2.1 SqlMapConfig.xml

**核心配置文件主要包含以下几个部分：**

* configuration

  * properties 属性
  * settings 设置
  * typeAliases 类型别名
  * typeHandlers 类型处理器
  * objectFactory 对象工厂
  * plugins 插件
  * environments 多环境配置

    * enviroment

      * transactionManager 事务管理器
      * dataSource 数据源
  * databaseIdProvider 数据库厂商标识
  * mappers 映射器

下面我们分别来看下这些配置在 mybatis 核心配置文件中的用途。

**environments 标签**

environments 标签主要用于数据源的配置

```xml
<!-- default 属性指定默认使用的数据源环境 -->
<enviroments default="development">
<!-- id 属性指定环境id -->
    <enviroment id="development">
	<!-- type 属性指定当前事务管理器类型 -->
        <transactionManager type="JDBC" />
	<!-- POOLED 表示当前数据源使用连接池管理连接 -->
        <dataSource type="POOLED">
            <property name="driver" value="" />
            <property name="url" value="" />
            <property name="username" value="" />
            <property name="password" value="" />
        </dataSource>
    </enviroment>
</enviroments>
```

transactionManager 标签的 type 属性有两种选项，分别为 JDBC 和 MANAGED，一般来说推荐直接使用 JDBC。

* JDBC：表示mybatis 使用 JDBC 的提交和回滚设置，它依赖从数据源得到的连接来管理事务作用域；
* MANAGED：这个配置几乎没做什么。

dataSource 的 type 属性也有如下几种配置：

* UNPOOLED：表示每次请求都重新打开和关闭连接；
* POOLED：使用连接池管理连接；
* JNDI：这个配置适合在 EJB 或应用服务器这类容器中使用。



## jdbc 问题分析

在介绍 mybatis 之前，我们先来看下下面这段代码：

```java
public void execute() {
    Connection connection = null;
    PreparedStatement preparedStatement = null;
    ResultSet resultSet = null;
    try {
        Class.forName("com.mysql.jdbc.Driver");
        connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/mybatis?characterEncoding=utf-8", "root", "root");
        String sql = "select * from user where username = ?";
        preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setString(1, "tom");
        resultSet = preparedStatement.executeQuery();
        while (resultSet.next()) {
            int id = resultSet.getInt("id");
            String username = resultSet.getString("username");
            user.setId(id);
            user.setUsername(username);
        }
        System.out.println(user);
    }
} catch (Exception e) {
    e.printStackTrace();
} finally {
    // 释放资源
}
```

这段代码是 jdbc 操作数据库的标准模板，虽然在逻辑上这段代码并没有任何问题，但是使用起来却非常不方便，其主要体现在以下几点：

* 调用该方法时会频繁的创建、释放连接，很消耗系统资源；
* sql 语句硬编码在代码中，造成代码不易维护；
* 使用 preparedStatement 向占位符传参存在硬编码，因为 sql 语句的 where 条件不一定，可能多也可能少，修改 sql 语句还需要修改代码，造成代码不易维护；
* 对结果集解析存在硬编码，sql 如果发生变化，解析代码也要随之发生变化，造成代码不易维护；

对于这几个问题，我们可以从以下几个不同的角度去解决：

1. 频繁创建、释放数据库连接问题，可以通过建立连接池来解决；
2. sql 语句和参数硬编码在代码中的问题，可以通过引入其他配置文件的方式，将 sql 语句写在配置文件中，和代码分离开来；
3. 结果集解析封装的问题，可以使用反射的方式来进行处理；
