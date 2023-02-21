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
