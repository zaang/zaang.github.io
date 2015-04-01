---
layout: post
category: java
title: Java Tutorial Note.1
tagline: 2015-03-15
tags: [java]
---

Java 的语法与 C++、C# 还是有许多类似的，先记录一下目前觉得要注意的地方。

<!--more-->

### 命名

- For all class names, the first letter should be in Upper Case.
- All method names should start with a Lower Case letter.
- Name of the program file should exactly match the class name.

### 代码结构

- There can be only one public class per source file.
- A source file can have multiple non public classes.
- The public class name should be the name of the source file as well which should be appended by .java at the end.

### 其他

enums can be declared as their own or inside a class. Methods, variables, constructors can be defined inside enums as well.

There is no default value for local variables so local variables should be declared and an initial value should be assigned before the first use.

A variable or method declared without any access control modifier is available to any other class in the same package. The fields in an interface are implicitly public static final and the methods in an interface are by default public.
Methods declared without access control (no modifier was used) can be declared more private in subclasses.