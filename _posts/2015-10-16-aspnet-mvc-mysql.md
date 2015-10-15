---
layout: post
category: windows
title: ---
layout: post
category: windows
title: ASP.NET MVC & MySQL
tagline: 2015-09-21
tags: [windows, mysql, asp.net]
---

ASP.NET MVC & MySQL 的环境搭建与配置的一些问题。

<!--more-->

开发环境：Windows10、VS2015

### 环境搭建

1. 安装 MySQL (ZIP) [http://dev.mysql.com/downloads/windows/installer/](http://dev.mysql.com/downloads/windows/installer/)

> 安装后修改 root 用户密码，比如改为 root：

    mysql -uroot -p
    use mysql
    update user set password=password("root") where user='root';
    flush privileges;

2. 安装 MySQL Connector/Net [http://dev.mysql.com/downloads/connector/net/](http://dev.mysql.com/downloads/connector/net/)

3. 安装 MySQL for Visual Studio [http://dev.mysql.com/downloads/windows/visualstudio/](http://dev.mysql.com/downloads/windows/visualstudio/)

4. VS 中 Nuget 安装 Entity Framework (6.1.3)

5. VS 中 Nuget 安装 MySQL.Data.Entity (6.9.7)，版本与 MySQL Connector/Net 一致

### 运行发生的问题

用的是 Code Frist 的方式，各种错误，总结如下：

1. Web.config 中检查 provider，用 nuget 安装过这里会自动改好。
2. Web.config 中增加 connectionStrings。
3. Global.asax.cs 中增加 Database.SetInitializer(...);

但是运行后仍报错 “Specified key was too long; max key length is 767 bytes”。

解决方法参考了 [http://stackoverflow.com/questions/24981593/...](http://stackoverflow.com/questions/24981593/specified-key-was-too-long-max-key-length-is-767-bytes-mysql-error-in-entity-fr)

在 MyContext 类上方添加 [DbConfigurationType(typeof(MySql.Data.Entity.MySqlEFConfiguration))]
在类构造函数添加 DbConfiguration.SetConfiguration(new MySql.Data.Entity.MySqlEFConfiguration())
