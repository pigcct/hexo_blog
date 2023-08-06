---
title: java编码规范
author: 苦逼小码农
tags:
  - 规范
categories:
  - Java
mathjax: true
date: 2023-05-12 11:35:56
---

# Java编码规范


>💡 俗话说： “没有规矩不成方圆”。 编程工作往往都是一个团队协同进行， 因而一致的编码规范非常有必要， 这样写成的代码便于团队中的其他人员阅读， 也便于编写者自己以后阅读。



## 命名规范

1. 主要的命名方法有一下两种
- 匈牙利命名， 一般只是命名变量， 原则是： 变量名 = 类型前缀 + 描述， 如bFoo表示布尔类型变量， pFoo表示指针类型变量。 匈牙利命名还是有一定争议的， 在Java编码规范中基本不被采用。
- 驼峰命名（Camel-Case） ， 又称“骆驼命名法”， 是指混合使用大小写字母来命名。 驼峰命名又分为小驼峰法和大驼峰法。 小驼峰法就是第一个单词是全部小写， 后面的单词首字母大写， 如myRoomCount； 大驼峰法是第一个单词的首字母也大写， 如ClassRoom。


>💡 除了包和常量外， Java编码规范命名方法采用驼峰法， 下面分类说明一下。

- 包名： 包名是全小写字母， 中间可以由点分隔开。 作为命名空间， 包名应该具有唯一性， 推荐采用公司或组织域名的倒置， 如com.apple.quicktime.v2。 但Java核心库包名不采用域名的倒置命名， 如java.awt.event。
- 类和接口名： 采用大驼峰法， 如SplitViewController。
- 文件名： 采用大驼峰法， 如BlockOperation.java。
- 变量： 采用小驼峰法， 如studentNumber。
- 常量名： 全大写， 如果是由多个单词构成， 可以用下划线隔开， 如YEAR和WEEK_OF_MONTH。
- 方法名： 采用小驼峰法， 如balanceAccount、 isButtonPressed等。

## eg:

```java
package com.a51work6;

public class Date extends java.util.Date {

private static final int DEFAULT_CAPACITY = 10;
private int size;

public static Date valueOf(String s) {
final int YEAR_LENGTH = 4;
final int MONTH_LENGTH = 2;
int firstDash;
int secondDash;
...
} 

public String toString () {
int year = super.getYear() + 1900;
int month = super.getMonth() + 1;
int day = super.getDate();
...
}
}
```

## Java注释


>💡 Java中注释的语法有三种： 单行注释（//） 、 多行注释（/*...*/） 和文档注释（/**...*/） 

>💡 代码注释一般是采用单行注释（//） 和多行注释（/*...*/）

**文件注释**

文件注释就是在每一个文件开头添加注释。文件注释通常包括如下信息:版权信息、文件名、所在模块、作者信息、历史版本信息、文件内容和作用等。

下面看一个文件注释的示例:
```txt
/*
*许可信息查看LICENSE.txt文件
*描述:
*实现日期基本功能
*历史版本:
*2015-7-22:创建文档
*2015-8-20:添加socket库
*2015-8-22:添加math库
*/
```

上述注释只是提供了版权信息、文件内容和历史版本信息等，文件注释要根据本身的实际情况包括内容。



### 文档注释


>💡 文档注释就是指这种注释内容能够生成API帮助文档， JDK中javadoc命令能够提取这些注释信息并生成HTML文件。 文档注释主要对类（或接口） 、 实例变量、 静态变量、 实例方法和静态方法等进行注释。

```java
package com.a51work6;
/**
* 自定义的日期类， 具有日期基本功能， 继承java.util.Date
* <p>实现日期对象和字符串之间的转换</p>
* @author 关东升
*/
public class Date extends java.util.Date {
private static final int DEFAULT_CAPACITY = 10;
/**
* 容量
*/
public int size;
/**
* 将字符串转换为Date日期对象
* @param s 要转换的字符串
* @return Date日期对象*/
public static Date valueOf(String s) {
final int YEAR_LENGTH = 4;
final int MONTH_LENGTH = 2;
int firstDash;
int secondDash;
...
} /
**
* 将日期转换为yyyy-mm-dd格式的字符串
* @return yyyy-mm-dd格式的字符串
*/
public String toString () {
int year = super.getYear() + 1900;
int month = super.getMonth() + 1;
int day = super.getDate();
...
}
}
```

### 文档注释标签



>💡 如果你想生成API帮助文档， 可以使用javadoc指令， 如图5-1所示， 在命令行中输入javadoc -d apidocData.java指令， -d参数指明要生成文档的目录， apidoc是当前目录下面的apidoc目录， 如果不存在javadoc会创建一个apidoc目录； Data.java是当前目录下的Java源文件。



### 地标注释


>💡 Eclipse等IDE工具都为Java源代码提供了一些特殊的注释， 就是在代码中加一些标识， 便于IDE工具快速定位代码， 称为“地标注释”。 这种注释虽然不是Java官方所提供的， 但是主流语言和主流的IDE工具也都支持“地标注释”。



### Eclipse工具支持如下三种地标注释：

- TODO： 说明此处有待处理的任务， 或代码没有编写完成。
- FIXME： 说明此处代码是错误的， 需要修正。
- XXX： 说明此处代码虽然实现了功能， 但是实现的方法有待商榷， 希望将来能改进。