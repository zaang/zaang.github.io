---
layout: post
category: Windows
title: Install MySQL on Win7
tagline: 2015-02-16
tags: [windows, database]
---

Windows 7 安装 MySql Server 时遇到了一些问题，记录一下。

<!--more-->

环境：Windows 7 SP 1, MySQL Server 5.6

### MySQL Command Line Client 启动一闪而过

编辑Command Line Client的快捷方式，查看启动目标发现"C:\Program Files\MySQL\MySQL Server 5.6\my.ini"不存在，使用Everything搜索定位到该文件位于"C:\ProgramData\MySQL\MySQL Server 5.6\my.ini"，按这个路径修改快捷方式后OK。

### 修改root用户默认密码

    c:\Program Files\MySQL\MySQL Server 5.6\bin>mysqladmin -u root password
    New password: ****
    Confirm new password: ****

### 安装MySQL服务

    c:\Program Files\MySQL\MySQL Server 5.6\bin>mysqld.exe install
    Service successfully installed.