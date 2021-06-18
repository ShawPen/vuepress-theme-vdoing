---
title: javase需要注意的
date: 2021-06-17 15:45:25
author: 
     name: shaw
sticky: 1
sidebar: auto
permalink: /pages/655a53/
categories:
  - 开始写blog了
tags:
  - 
---
## java程序运行过程
1. java程序的编译
    - 程序员需要在计算机硬盘中新建.java文件，查看.java文件是否符合java语法规则，如果符合就把.java文件编译为.class的字节码文件
    - java程序员需要使用javac.exe（java编译器）将.java文件将编译为.class。
    - 一个java源文件可以生成多个.class（字节码文件）文件。最终执行的时.class文件。
2. 运行阶段
    - 使用java.exe运行字节码文件。
    - 使用命令：
        ```
        java 类名
        ```
    - java.exe启动JVM，JVM会启动classLoader
    - classloader会去硬盘上搜索.class文件，找到字节码文件后，会将字节码文件装入JVM
    - JVM将字节码文件解释成二进制数据
    - 然后操作系统执行二进制文件和底层硬件平台进行交互。

## JDK、JRE、JVM之间的关系
JRE是Java程序能够执行的环境，里面包含了JVM，如果不是开发人员，只需要在电脑中运行Java程序，那么就可以只安装JRE；而JDK是java开发的环境，如果是作为开发java的程序员，就必须安装JDK。

## class和public class
- 一个java源文件中可以定义多个class
- 一个java文件中的public class不是必须的
- 一个class可以生成一个.class文件。
- 一个java源文件中定义公开的类的话，只能有一个，并且该类的名字必须和源文件的名字一致。

## java程序在运行时的内存结构
- 在JVM中有三个存储区域
    - 方法区（.class文件中的代码块。静态变量，静态代码块转移到堆）
    - 堆（new 出的对象，以及实例变量，静态变量和静态代码块）
    - 栈（方法运行时压栈，结束时出栈，局部变量的存储。）

## 静态代码块和实例代码块
- 静态代码块在类加载的时候调用
- 实例代码块在new 时，构造方法之前执行。

## java代码执行的顺序
- 方法体中有顺序
- 静态代码块之间有顺序
- 静态代码块和静态变量有顺序

## 反射机制
- 反射机制可以操作字节码文件
- 与反射机制有关的类
    - java.lang.Class字节码文件
    - java.lang.reflect.Method字节码方法
    - java.lang.reflect.Consructor字节码构造方法
    - java.lang.reflect.field字节码属性
- 三种获取字节码文件的方式

获取字节码文件的方式 | 类和方法
---|---
方式一 | Class.forName("");参数为完整类名
方式二 | 对象名.getClass();
方式三 | 对象名.class;

- 通过Class对象的.newInstance方法可以实例化对象。
    ```
    Class对象.newInstance()
    ```
- 反射机制的灵活性

  java程序只写一次，在不改变java源代码的情况下，可以做到不同的对象的实例化。非常灵活，（符合开闭原则，对扩展开放，对修改关闭）
  使用properties文件配置（以键值对的形式）
  ```java
    package com.test.example;
    import java.io.FileReader;
    import java.util.Properties;

    public class App {

        public static void main(String[] args) throws Exception{
            FileReader fileReader = new FileReader("test.properties");
            Properties properties = new Properties();
            properties.load(fileReader);
            fileReader.close();
            String ClassName = properties.getProperty("classname");
            System.out.println(ClassName);
            Class obj = Class.forName(ClassName);//得到class文件
            Object object = obj.newInstance();
            System.out.println(object);

        }
    }
    ```
    test.properties里面的内容是可以改变的

    ```properties
    classname=java.util.Date
    ```
    
## 获取当前的绝对路径
```java
    String path = Thread.currentThread().getContextClassLoader()
                .getResource("test.properties").getPath();
```
该代码可以跨平台使用        
   <img src="/img/bg.jpeg"/> 

    



