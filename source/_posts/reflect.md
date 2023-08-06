---
title: 反射
author: 苦逼小码农
tags:
  - 反射
categories:
  - Java
mathjax: true
date: 2023-06-04 21:56:20
---

# 反射机制



## 1. 什么是反射

在Java中，反射是指能够在运行时获取类的信息并操作类或对象的能力。通过反射，可以获取类的名称、属性、方法等信息，也可以动态地创建对象、调用方法等。Java中的反射机制提供了很多灵活性和可扩展性，但也需要注意反射操作可能会影响程序的性能和安全性。

{% asset_img 1.png %}



**通过反射可以获取class(字节码文件)，构造方法，成员变量和成员方法**

{% asset_img 2.png %}







## 2. 获取



### 2.1 获取Class对象

1. 通过全类名 Class.forName("全类名")获取
2. 通过类名.class获取
3. 通过对象.getClass() 获取



{% asset_img 3.png %}



```java
package com.reflect.sty;

public class MyReflect01 {
    public static void main(String[] args) throws ClassNotFoundException {
        /*
         * 获取Class对象的三种方式
         *   1.Class.forName("全类名");
         *   2.类名.class
         *   3.对象.getClass();
         * */

        // 1.第一种方式 Class.forName("全类名");
        // 全类名字：包名 + 类名
        Class clazz = Class.forName("com.reflect.sty.Student");
        System.out.println(clazz);
        System.out.println("--------------------------------------------");

        // 2.第二种方式 类名.class
        // 一般当作参数进行传递
        Class<Student> clazz2 = Student.class;
        System.out.println(clazz2);
        System.out.println("--------------------------------------------");

        // 3.第三种方式 对象.getClass();
        // 当我们有对象时，才能进行使用
        Student student = new Student();
        Class<? extends Student> clazz3 = student.getClass();
        System.out.println(clazz3);
        System.out.println("--------------------------------------------");

        System.out.println(clazz == clazz2 && clazz == clazz3);

    }

}

```





### 2.2 获取构造方法

**Class中用于获取构造方法的方法**

1. Constructor<?> [] getConstructors():返回所有公共构造方法对象的数组
2. Constructor<?> [] getDeclaredConstructors():返回所有构造方法对象的数组
3. Constructor<T> getConstructor(Class<?>... parameterTypes):返回单个公共构造方法对象
4. Constructor<T>getDeclaredConstructor(Class<?>... parameterTypes):返回单个构造方法对象



**Constructor类中用于创建对象的方法**

1. T newlnstance(Object... initargs):根据指定的构造方法创建对象
2. setAccessible(boolean flag):设置为true,表示取消访问检查



```java
package com.reflect.sty.test02;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Parameter;

public class MyReflect {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
     
        // 1.获取class字节码文件对象
        Class clazz = Class.forName("com.reflect.sty.test02.Student");

        // 2.获取构造方法

        // 2.1 返回公共构造方法对象的数组
 /*       Constructor[] cons = clazz.getConstructors();
        for (Constructor con : cons) {
            System.out.println(con);
        }*/

        // 2.2 返回所有构造方法对象的数组

/*        Constructor[] cons2 = clazz.getDeclaredConstructors();
        for (Constructor con : cons2) {
            System.out.println(con);
        }*/


        // 2.3 返回单个构造方法的对象（Declared --> 权限符：可以返回public，也可以返回private）
/*        Constructor con1 = clazz.getDeclaredConstructor();
        System.out.println(con1);

        Constructor con2 = clazz.getConstructor(String.class);
        System.out.println(con2);

        Constructor con3 = clazz.getDeclaredConstructor(int.class);
        System.out.println(con3);*/

        Constructor con4 = clazz.getDeclaredConstructor(String.class, int.class);
        System.out.println(con4);
        System.out.println("---------");

        // 返回权限修饰符
        //  public：1  private：2  protected：4
/*        int modifiers = con4.getModifiers();
        System.out.println(modifiers);*/

        // idea可以使用 Ctrl+ P 可以求出方法的参数的类型
/*        Parameter[] parameters = con4.getParameters();
        for (Parameter parameter : parameters) {
            System.out.println(parameter);
        }*/

        // 暴力反射：表示临时取消权限校验
        con4.setAccessible(true);
        Student stu = (Student) con4.newInstance("香辣小猪", 123);

        System.out.println(stu);
    }

}

```



```java
package com.reflect.sty.test02;

public class Student {
    private String name;
    private int age;

    public Student() {
    }

    public Student(String name) {
        this.name = name;
    }

    protected Student(int age) {
        this.age = age;
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    public String toString() {
        return "Student{name = " + name + ", age = " + age + "}";
    }
}

```



### 2.3 获取成员变量

**Class类中用于获取成员变量的方法**

1. Field[] getFields():返回所有公共成员变量对象的数组
2. Field[ ] getDeclaredFields():返回所有成员变量对象的数组
3. Field getField(String name):返回单个公共成员变量对象
4. Field getDeclaredField(String name):返回单个成员变量对象



**Field类中用于创建对象的方法**

1. void set(Object obj, Object value):赋值
2. Object get(Object obj)获取值



```java
package com.reflect.sty.test03;

import java.lang.reflect.Field;

public class MyReflect {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException, IllegalAccessException {

        // 1.获取class字节码文件的对象
        Class clazz = Class.forName("com.reflect.sty.test03.Student");

        // 2.获取所有成员变量
 /*       Field[] fields = clazz.getDeclaredFields();
        for (Field field : fields) {
            System.out.println(field);
        }*/

        // 获取当个成员变量
        Field name = clazz.getDeclaredField("name");
        System.out.println(name);

        // 3.获取权限修饰符
        int modifiers = name.getModifiers();
        System.out.println(modifiers);

        // 4.获取成员变量的名字
        String n = name.getName();
        System.out.println(n);

        // 5.获取成员变量的数据类型
        Class<?> type = name.getType();
        System.out.println(type);
        System.out.println("-------------------------");

        
        // 6.获取成员变量记录的值
        Student student = new Student("spicypig", 23, "男");
        System.out.println(student);
        name.setAccessible(true);
        Object value = name.get(student);
        System.out.println(value);

        // 修改对象里面记录的值
        name.set(student, "香辣小猪");

        System.out.println(student);

    }
}

```





```java
	package com.reflect.sty.test03;

public class Student {
    private String name;
    private int age;
    public String gender;


    public Student() {
    }

    public Student(String name, int age, String gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    /**
     * 获取
     * @return gender
     */
    public String getGender() {
        return gender;
    }

    /**
     * 设置
     * @param gender
     */
    public void setGender(String gender) {
        this.gender = gender;
    }

    public String toString() {
        return "Student{name = " + name + ", age = " + age + ", gender = " + gender + "}";
    }
}

```





### 2.4 获取成员方法



**Class类中用于获取成员方法的方法**

1. Method[ ] getMethods():返回所有公共成员方法对象的数组，包括继承的
2. Method[] getDeclaredMethods():返回所有成员方法对象的数组，不包括继承的
3. Method getMethod(String name, Class<?>... parameterTypes):返回单个公共成员方法对象
4. Method getDeclaredMethod(String name, Class<?>... parameterTypes):返回单个成员方法对象



**Method类中用于创建对象的方法**

1. Object invoke(Object obj, Object... args):运行方法参数一:用obj对象调用该方法
   参数二:调用方法的传递的参数（如果没有就不写)返回值:方法的返回值（如果没有就不写)



```java
package com.reflect.sty.test04;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.lang.reflect.Parameter;

public class MyReflect {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, IllegalAccessException {

        // 1. 获取class字节码文件对象
        Class<?> clazz = Class.forName("com.reflect.sty.test04.Student");

        // 2.获取所有对象的方法（getMethods 包含父类中所有的公共方法）
/*        Method[] methods = clazz.getMethods();
        for (Method method : methods) {
            System.out.println(method);
        }*/

        // 获取所有对象的方法（不能获取父类，当时可以获取本类中私有的方法）
        Method[] methods = clazz.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println(method);
        }

        // 3.获取指定的单一方法
        Method m = clazz.getDeclaredMethod("eat", String.class);
        System.out.println(m);

        // 4.获取方法的修饰符
        int modifiers = m.getModifiers();
        System.out.println(modifiers);

        // 5.获取方法的名字
        String name = m.getName();
        System.out.println(name);

        // 6.获取方法形参
        Parameter[] parameters = m.getParameters();
        for (Parameter parameter : parameters) {
            System.out.println(parameter);
        }

        // 7.获取方法抛出的异常
        Class[] exceptionTypes = m.getExceptionTypes();
        for (Class exceptionType : exceptionTypes) {
            System.out.println(exceptionType);
        }

        // 8.运行获取的方法（得到方法的返回值）
/*        Method类中用于创建对象的方法
          Object invoke(Object obj, Object... args)的运行方法：
          参数一：用obj对象调用方法
          参数二：调用发的传递的参数（没有不写）
          返回值：方法返回值（没有不写）
                */
        Student student = new Student();
        m.setAccessible(true);

        // 参数一（s）:表示方法的调用者
        // 参数二（“汉堡包”）:表示在调用方法的时候传递的实际参数
        String res = (String) m.invoke(student, "汉堡包");
        System.out.println(res);
    }
}

```





```java
package com.reflect.sty.test04;

import java.io.IOException;

public class Student {
    private String name;
    private int age;


    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    public void sleep() {
        System.out.println("睡觉");
    }

    private String eat(String s) throws IOException, NullPointerException, ClassCastException {
        System.out.println("吃" + s);
        return "奥利给";
    }

    private void eat(String s, int a) {
        System.out.println("吃" + s);
    }

    public String toString() {
        return "Student{name = " + name + ", age = " + age + "}";
    }
}

```









## 3. 反射的作用

1. 获取一个类里面所有的信息，获取到了之后，再执行其他的业务逻辑。

2. 结合配置文件，动态的创建对象并调用方。

3. 动态地获取类的信息：可以在运行时获取类的名称、属性、方法等信息，而不需要在编译时就确定。
4. 动态地创建对象：可以根据类的名称动态地创建对象，而不需要在编译时就确定。
5. 动态地调用方法：可以在运行时根据方法名和参数列表动态地调用方法，而不需要在编译时就确定。
6. 实现通用框架：通过反射机制，可以编写通用的框架，使得框架可以处理各种类型的对象。
7. 实现动态代理：通过反射机制，可以实现动态代理，使得代理对象可以在运行时动态地生成。





## 4.练习

### 4.1 练习一

**对于任意一个对象，都可以把对象所有的字段名和值，保存到文件中去**

{% asset_img 4.png %}



#### MyReflect

```java
package com.reflect.sty.zlx01;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.lang.reflect.Field;

public class MyReflect {
    public static void main(String[] args) throws IllegalAccessException, IOException {

        /*
        要求：对于任意一个对象，都可以吧对象所有的字段名和值，保存到文件中去
        */

        Student student = new Student("Tom", 23, '女', 186.7, "学习");
        Teacher teacher = new Teacher("波妞", 10000);


        saveObject(student);

    }


        // 把对象里面所有的成员变量和值保存到本地文件中

        public static void saveObject(Object obj) throws IllegalAccessException, IOException {

            // 1.获取字节码文件的对象
            Class clazz = obj.getClass();


            // 2. 创建IO流
            BufferedWriter bw = new BufferedWriter(new FileWriter("src/com/student.txt"));


            // 2.获取所有的成员变量
            Field[] fields = clazz.getDeclaredFields();
            for (Field field : fields) {
                //  临时校验
                field.setAccessible(true);

                // 获取成员变量的名字
                String name = field.getName();

                // 获取成员变量的值
                Object value = field.get(obj);

                // 写出数据
                bw.write(name + "=" + value);
                bw.newLine();

            }
            System.out.println("写入成功");
            bw.close();

        }


}

```



#### Student

```java
package com.reflect.sty.zlx01;

public class Student {
    private String name;
    private int age;
    private char gender;
    private double height;
    private String hobby;


    public Student() {
    }

    public Student(String name, int age, char gender, double height, String hobby) {
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.height = height;
        this.hobby = hobby;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    /**
     * 获取
     * @return gender
     */
    public char getGender() {
        return gender;
    }

    /**
     * 设置
     * @param gender
     */
    public void setGender(char gender) {
        this.gender = gender;
    }

    /**
     * 获取
     * @return height
     */
    public double getHeight() {
        return height;
    }

    /**
     * 设置
     * @param height
     */
    public void setHeight(double height) {
        this.height = height;
    }

    /**
     * 获取
     * @return hobby
     */
    public String getHobby() {
        return hobby;
    }

    /**
     * 设置
     * @param hobby
     */
    public void setHobby(String hobby) {
        this.hobby = hobby;
    }

    public String toString() {
        return "Student{name = " + name + ", age = " + age + ", gender = " + gender + ", height = " + height + ", hobby = " + hobby + "}";
    }
}

```





#### Teacher

```java
package com.reflect.sty.zlx01;

public class Teacher {
    private String name;
    private double salary;


    public Teacher() {
    }

    public Teacher(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return salary
     */
    public double getSalary() {
        return salary;
    }

    /**
     * 设置
     * @param salary
     */
    public void setSalary(double salary) {
        this.salary = salary;
    }

    public String toString() {
        return "Teacher{name = " + name + ", salary = " + salary + "}";
    }
}

```







### 4.2 练习二

**反射可以更配置文件结合的方式，动态的创建对象，并调用方法**



#### MyReflect

```java
package com.reflect.sty.zlx02;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.Properties;

public class MyReflect {
    public static void main(String[] args) throws IOException, ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        /*
        要求：发射可以配置文件结合的方式，动态的创建对象，并且调用方法
        */

        // 1.读取配置文件中的信息
        Properties p = new Properties();
        FileInputStream fis = new FileInputStream("src/com/prop.properties");
        System.out.println(p);
        p.load(fis);
        fis.close();
        System.out.println(p);

        // 2.获取全类名和方法名
        String className = (String) p.get("classname");
        String methodName = (String) p.get("method");

        System.out.println(className);
        System.out.println(methodName);

        // 3.利用反射创建对象并运行方法
        Class clazz = Class.forName(className);

        // 获取构造方法
        Constructor con = clazz.getDeclaredConstructor();
        Object o = con.newInstance();
        System.out.println(o);

        // 获取成员方法并且运行
        Method method = clazz.getDeclaredMethod(methodName);
        method.setAccessible(true);
        method.invoke(o);


    }
}

```





#### Student



```java
package com.reflect.sty.zlx02;

public class Student {
    private String name;
    private int age;


    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void study() {
        System.out.println("学生正在学习！");
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    public String toString() {
        return "Student{name = " + name + ", age = " + age + "}";
    }
}

```



#### Teacher

```java
package com.reflect.sty.zlx02;

public class Teacher {
    private String name;
    private double salary;


    public Teacher() {
    }

    public Teacher(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public void teach() {
        System.out.println("老师正在教书！");
    }

    /**
     * 获取
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     * @return salary
     */
    public double getSalary() {
        return salary;
    }

    /**
     * 设置
     * @param salary
     */
    public void setSalary(double salary) {
        this.salary = salary;
    }

    public String toString() {
        return "Teacher{name = " + name + ", salary = " + salary + "}";
    }
}

```



#### 配置文件

```txt
classname=com.reflect.sty.zlx02.Teacher
method=teach
```





## 5. 动态代理











