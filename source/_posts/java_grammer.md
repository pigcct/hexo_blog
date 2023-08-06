---
title: java基础语法
author: 苦逼小码农
tags:
  - 语法
categories:
  - Java
mathjax: true
date: 2023-05-12 11:35:56
---

# Java基础语法

## 1. 标识符，关键字和保留字
### 1.1 标识符

标识符就是变量、常量、方法、枚举、类、接口等由程序员指定的名字。构成标识符的字母均有一定的规范，Java语言中标识符的命名规则如下：

- 区分大小写：Myname与myname是两个不同的标识符。
- 首字符，可以是下划线（_）或美元符或字母，但不能是数字。
- 除首字符外其他字符，可以是下划线（_）、美元符、字母和数字。
- 关键字不能作为标识符。
- 

### 1.2 java关键字

> Java中的关键字全部是小写字母



{% asset_image 1.jpg %}



### 1.3 保留字
Java中有一些字符序列既不能当作标识符使用，也不是关键字，也不能在程序中使用，这些字符序列称为保留字。Java语言中的保留字只有两个goto和const：

- goto：在其他语言中叫做“无限跳转”语句，在Java语言中不再使用goto语句，因为“无限跳转”语句会破坏程序结构。在Java语言中goto的替换语句可以通过break、continue和return实现“有限跳转”。

- const：在其他语言中是声明常量关键字，在Java语言中声明常量使用public static final 方式声明。

> java分隔符：用";"表示一条语句的结束


## 2. 常量，变量
### 2.1 常量

> 💡 final 数据类型 变量名 = 初始值;

```java
public class HelloWorld {
  // 静态常量，替代保留字const
  public static final double PI = 3.14; ①
  // 声明成员常量
  final int y = 10; ②
  public static void main(String[] args) {
  // 声明局部常量
  final double x = 3.3; ③
  }
}
```

**常量有三种类型：①静态常量、②成员常量和③局部常量**

### 2.2 变量

> 💡 数据类型  变量名 = [初始值]


```java
public class HelloWorld {
// 声明int型成员变量
int y; ①
public static void main(String[] args) {
// 声明int型局部变量
int x; ②
// 声明float型变量并赋值
float f = 4.5f; ③
// x = 10;
System.out.println("x = " + x);// 编译错误，局部变量 x未初始化 ④
System.out.println("f = " + f);
if (f < 10) {
// 声明型局部变量
int m = 5; ⑤
}
System.out.println(m); // 编译错误 ⑥
}
}
```

- 第①行是声明的成员变量y，成员变量是在类体中，而在方法之外，作用域是整个类，如果没有初始赋值，系统会为它分配一个默认值，每一种数据类型都有默认值，int类型默认值是0。
- 第②和③行声明局部变量作用域是整个方法
- 第⑤行声明的m变量作用域是当前的if语句。
- 第④行和第⑥行会有编译错误方法，因为没有初始化，局部变量使用前是需要进行初始化的




## 3. 数据类型
> 💡 Java语言的数据类型分为： 基本类型和引用类型。在声明变量或常量时会用到数据类型， 在前面已经用到一些数据类型， 例如int、 double和String等。
### 3.1 基本数据类型

{% asset_image 10.png %}

***基本类型表示简单的数据， 基本类型分为4大类， 共8种数据类型。***

- 整数类型： byte、 short、 int和long
- 浮点类型： float和double
- 字符类型： char
- 布尔类型： boolean



{% asset_image 2.png 数据类型之间的转换关系%}



#### 3.1.1 整形类型

> 💡如图可见Java中整数类型包括： byte、 short、 int和long ， 它们之间的区别仅仅是宽度和范围的不同。 Java中整数都是有符号， 与C不同没有无符号的整数类型。



{%asset_image 3.png %}



> 💡 long类型需要在数值后面加L, double类型加D, float类型加F

**代码如下：**

```java
public class HelloWorld {
  public static void main(String[] args) {
    // 声明整数变量
    // 输出一个默认整数常量
    System.out.println("默认整数常量 = " + 16); //此处16默认为整数类型
    byte a = 16; 
    short b = 16; 
    int c = 16; 
    //long类型后面加l或L，l容易混淆，建议加L
    long d = 16L; 
    long e = 16l; 
    System.out.println("byte整数 = " + a);
    System.out.println("short整数 = " + b);
    System.out.println("int整数 = " + c);
    System.out.println("long整数 = " + d);
    System.out.println("long整数 = " + e);
  }
}
```

#### 3.1.2 浮点类型
> 💡浮点类型主要用来储存小数数值， 也可以用来储存范围较大的整数。 它分为浮点数（float） 和双精度浮点数（double） 两种， 双精度浮点数所使用的内存空间比浮点数多， 可表示的数值范围与精确度也比较大

|浮点类型|宽度|
|---|:---:|
|float|4字节（32位）|
|double|8字节（64位）|

* Java语言浮点类型默认是double类型， 例如0.0表示double类型常量， 而不是float类型。 如果想要表示float类型， 则需要在数值后面加f或F 

```java
public class HelloWorld {
	public static void main(String[] args) {
		// 声明浮点数
		// 输出一个默认浮点常量
		System.out.println("默认浮点常量 = " + 360.66); 
		float myMoney = 360.66f; 
		double yourMoney = 360.66; 
		final double PI = 3.14159d; 
		System.out.println("float整数 = " + myMoney);
		System.out.println("double整数 = " + yourMoney);
		System.out.println("PI = " + PI);
	}
}
```
#### 3.1.3 字符类型

> 💡字符类型表示单个字符， Java中char声明字符类型， Java中的字符常量必须用单引号括起来的单个字符 ，如char c = 'A';

{% asset_image 4.png 转义字符%}

#### 3.1.4 布尔类型

> 💡在Java语言中声明布尔类型的关键字是boolean， 它只有两个值： true和false。不能与int等数值类型之间进行数学计算或类型转化。

```java
//唯一正确的两种赋值方式
boolean isMan = true;
boolean isWoman = false;
```



### 3.2 数字的表示方法

#### 3.2.1 进制数字的表示

如果为一个整数变量赋值， 使用二进制数、 八进制数和十六进制数表示， 它们的表示方式分别如下：

- 二进制数： 以 0b 或0B为前缀， 注意0是阿拉伯数字， 不要误认为是英文字母o。
- 八进制数： 以0为前缀， 注意0是阿拉伯数字。
- 十六进制数： 以 0x 或0X为前缀， 注意0是阿拉伯数字。
```java
//int型28的不同表示方法
int decimalInt = 28;
//二进制
int binaryInt1 = 0b11100;
int binaryInt2 = 0B11100;
//八进制
int octalInt = 034;
//十六进制
int hexadecimalInt1 = 0x1C;
int hexadecimalInt2 = 0X1C;
```

#### 3.2.2 指数表示
> 💡如果采用十进制表示指数， 需要使用大写或小写的e表示幂， e2表示102。

```java
//表示为3.36×10^2
double myMoney = 3.36e2;
//表示为1.56×10^(-2)
double interestRate = 1.56e-2;
```



#### 3.3.3 数值类型的转换

**自动转换类型**：

自动类型转换就是需要类型之间转换是自动的，不需要采取其他手段，总的原则是小范围数据类型可以自动转换为大范围数据类型，列类型转换顺序如图所示，从左到右是自动。
{% asset_image 5.jpg %}

**计算过程中自动类型转换规则**

{% asset_image 6.jpg %}

**代码如下：**

```java
// 声明整数变量
byte byteNum = 16;
short shortNum = 16;
int intNum = 16;
long longNum = 16L;

// byte类型转换为int类型
intNum = byteNum;
// 声明char变量char charNum = '花';
// char类型转换为int类型
intNum = charNum;
// 声明浮点变量
// long类型转换为float类型
float floatNum = longNum;
// float类型转换为double类型
double doubleNum = floatNum;
//表达式计算后类型是double
double result = floatNum * intNum + doubleNum / shortNum;
```

### 3.3 强制类型转换

***强制类型转换是在变量或常量之前加上“(目标类型)”实现， 示例代码如下：***
```java
//int型变量
int i = 10;
//把int变量i强制转换为byte
byte b = (byte) i;
```

```java
//int型变量
int i = 10;
//把int变量i强制转换为byte
byte b = (byte) i;
int i2 = (int)i; ①
int i3 = (int)b;
```

**引用数据类型（包含： 类、 接口和数组声明的数据类型）**

{% asset_image 7.png %}
> 💡Java中的引用数据类型， 相当于C等语言中指针（pointer） 类型， 引用事实上就是指针， 是指向一个对象的内存地址。 引用数据类型变量中保持的是指向对象的内存地址。 很多资料上提到Java不支持指针， 事实上是不支持指针计算， 而指针类型还是保留了下来， 只是在Java中称为引用数据类型。

**引用数据类型实例如下**

```java
int x = 7;①
int y = x;②

String str1 = "Hello";③
String str2 = str1;④
str2 = "World";⑤
```


上述代码声明了两个基本数据类型(int）和两个引用数据类型(String)。当程序执行完第②行代码后，x值为7，x赋值给y，这时y的值也是7，它们的保持方式如图6-4所示，x和y两个变量值都是7，但是它们之间是独立的，任何一个变化都不会影响另一个。


当程序执行完第③行时，字符串“Hello”对象被创建，保持到内存地址0x12345678中，str1是引用类型变量，它保存的是内存地址Ox12345678，这个地址指向"Hello”对象。


当程序执行完第④行时，str1变量内容（Ox12345678）被赋值给str2是引用类型变量，这样一来str1和str2保存了相同的内存地址，都指向"Hello”对象。见图6-4所示，此时str1和str2本质上是引用一个对象，通过任何一个引用都可以修改对象本身。


当程序执行完第⑤行时，字符串“World”对象被创建，保持到内存地址0x23455678中，地址保存到str2变量中，此时，str1和str2不再指向相同内存地址，见图6-5所示。







  






## 4.运算符

### 4.1 算数运算符

> Java中的算术运算符主要用来组织数值类型数据的算术运算， 按照参加运算的操作数的不同可以分为一元运算符和二元运算符。

**一元运算符**

{% asset_image 11.png %}



***i ++ 和 ++ i的区别：***

* i ++ 是先赋值再自加

```java
int i = 1;
System.out.println( i ++) //  i = 1
```

* ++ i 是先自加再赋值

```java
int i = 1;
System.out.println( ++ i) //  i = 2
```



**二级运算符**

{% asset_image 12.png %}





### 4.2 关系运算符

> 关系运算是比较两个表达式大小关系的运算， 它的结果是布尔类型数据， 即true或false。 关系运算符有6种： ==、 !=、 >、 <、 >=和<=

{% asset_image 13.png %}







### 4.3 逻辑运算符

> 💡 逻辑运算符是对布尔型变量进行运算， 其结果也是布尔型



{% asset_image 14.png %}

### 4.4 位运算符

> 位运算是以二进位（bit） 为单位进行运算的， 操作数和结果都是整型数据。 位运算符有如下几个运算符： &、 |、 ^、 ~、 >>、 <<和>>>， 以及相应的赋值运算符



{% asset_image 15.png %}



***注意 无符号右移>>>运算符仅被允许用在int和long整数类型, 如果用于short或byte数据, 则数据在位移之前， 转换为int类型后再进行位移计算。***

**代码演示：**

```java
byte a = 0B00110010; //十进制50 ①
byte b = 0B01011110; //十进制94 ②
System.out.println("a | b = " + (a | b)); // 0B01111110 ③
System.out.println("a & b = " + (a & b)); // 0B00010010 ④
System.out.println("a ^ b = " + (a ^ b)); // 0B01101100 ⑤
System.out.println("~b = " + (~b)); // 0B10100001 ⑥
System.out.println("a >> 2 = " + (a >> 2)); // 0B00001100 ⑦
System.out.println("a >> 1 = " + (a >> 1)); // 0B00011001 ⑧
System.out.println("a >>> 2 = " + (a >>> 2)); // 0B00001100 ⑨
System.out.println("a << 2 = " + (a << 2)); // 0B11001000 ⑩
System.out.println("a << 1 = " + (a << 1)); // 0B01100100 ⑪
int c = -12; ⑫
System.out.println("c >>> 2 = " + (c >>> 2)); ⑬
System.out.println("c >> 2 = " + (c >> 2)); ⑭
```



**输出结果：**

```txt
a | b = 126
a & b = 18
a ^ b = 108
~b = -95
a >> 2 = 12
a >> 1 = 25
a >>> 2 = 12
a << 2 = 200
a << 1 = 100
c >>> 2 = 1073741821
c >> 2 = -3
```

- 上述代码第①行和第②行分别定义了byte变量a和b， 为了便于查看代码采用二进制整数表示。
- 代码第③行中表达式(a | b)进行位或运算， 结果是二进制的0B01111110。 a和b按位进行或计算， 只要有
- 一个为1， 这一位就为1， 否则为0。代码第④行(a & b)是进行位与运算， 结果是二进制的0B00010010。 a和b按位进行与计算， 只有两位全
- 部为1， 这一位才为1， 否则为0。代码第⑤行(a ^ b)是进行位异或运算， 结果是二进制的0B01101100。 a和b按位进行异或计算， 只有两
- 位相反时这一位才为1， 否则为0。代码第⑦行(a >> 2)是进行有符号右位移2位运算， 结果是二进制的0B00001100。 a的低位被移除掉， 由
- 于是正数符号位是0， 高位空位用0补。 类似代码第⑧行(a >> 1)是进行右位移1位运算， 结果是二进制的0B00011001。
- 代码第⑨行(a >>> 2)是进行无符号右位移2位运算， 与代码第⑦行不同的是， 无论是否有数符号位， 高位空位用0补， 所以在正数情况下>>和>>>运算结果是一样的。
- 代码第⑩行(a << 2)是进行左位移2位运算， 结果是二进制的0B11001000。 a的高位被移除掉， 低位用0补位。 类似代码第⑪行(a << 1)是进行左位移1位运算， 结果是二进制的0B01100100。
- 代码第⑫声明int类型负数。 右位移（>>>和>>） 在负数情况下差别比较大。 代码第⑬行的(c >>> 2)表达式输出结果是1073741821， 这是一个如此大的正数， 从一个负数变成一个正数， 这说明无符号右位移对于负数计算会导致精度的丢失。 而有符号右位移对于负数的计算是正确的， 见代码第⑭行。

> 提示 有符号右移n位， 相当于操作数除以2n， 例如代码第⑦行(a >> 2)表达式相当于(a / 22)， a =50所以结果等于12， 类似的还有代码第⑧行和第⑭行。 另外， 左位移n位， 相当于操作数乘以2n，例如代码第⑩行(a << 2)表达式相当于(a * 22)， a = 50所以结果等于200， 类似的还有代码第⑪行。



### 4.5 三元运算符

> 三元运算符（ a ?  b : c ) --> 表示 a表达式是否成立，成立的话执行b语句，否则执行c语句



**示例代码：**

```java
import java.util.Date;
public class HelloWorld {
public static void main(String[] args) {
int score = 80;
String result = score > 60 ? "及格" : "不及格"; // 三元运算符（? : ）
System.out.println(result);
Date date = new Date(); // new运算符可以创建Date对象
System.out.println(date.toString()); //通过.运算符调用方法
}
}
```



### 4.6 运算符优先级
>运算符优先级

{% asset_image 3.jpg %}

> 总结 运算符优先级大体顺序， 从高到低是： 算术运算符→位运算符→关系运算符→逻辑运算符→赋值运算符。

## 5. 控制语句

### 5.1 while循环

### 5.2 for循环

### 5.3 循环的嵌套

### 5.4 跳出循环





## 6.数组









