---
title: 多线程编程
author: 苦逼小码农
tags:
  - 多线程
categories:
  - Java
mathjax: true
date: 2023-05-25 20:41:30
---

# 多线程编程

## 1. 线程和进程

### 1.1 线程

线程是操作系统能够进行运算调度的最小单位。它被包含在进程之中，是进程中的实际运作单位。



### 1.2 进程

进程是程序的基本执行实体。



## 2. 并发和并行

### 2.1 并发

在同一时刻，有多个指令在单个CPU上**交替**执行。



### 2.2 并行

在同一时刻，有多个指令在单个CPU上**同时**执行。



## 3. 多线程的实现方式

**多线程的三种实现方式对比：**

{% asset_img 1.png %}



**常见的成员方法：**

{% asset_img 2.png %}



### 3.1 继承Thread类的方式实现

```java
package com.study.Test1;

public class ThreadDemo1 {
    public static void main(String[] args) {
        /*
        * 多线程的第一种启动方法
        * 1. 自己定义一个类继承Thread
        * 2. 重写run方法
        * 3. 创建子类的对象并且启动线程
        *
        * */
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();

        t1.setName("线程1");
        t2.setName("线程2");
        // 开启线程
        t1.start();
        t2.start();

    }
}

```





```java
package com.study.Test1;

public class MyThread extends Thread {

    @Override
    public void run() { // 书写线程执行的代码
        for (int i = 1; i <= 30; i++) {
            System.out.println(getName() + "第" + i + "次执行");
        }
    }
}

```





### 3.2 实现Runnable接口的方式实现

```java
package com.study.Test1;

public class ThreadDeom2 {
    public static void main(String[] args) {
        /*
         * 多线程的第二种启动方法
         * 1. 自己定义一个类实现Runnable接口
         * 2. 重写run方法
         * 3. 创建自己的类的对象
         * 4. 创建一个Thread对象并开启线程
         *
         * */

        // 创建自己的类（MyRun类）的对象
        MyRun mr = new MyRun();

        // 创建线程对象
        Thread t1 = new Thread(mr);
        Thread t2 = new Thread(mr);

        // 给线程设置名字
        t1.setName("线程1");
        t2.setName("线程2");

        // 开启线程
        t1.start();
        t2.start();

    }
}

```





```java
package com.study.Test1;

public class MyRun implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            /* Thread t = new Thread.currentThread();
             System.out.println(t.getName() + "执行了");*/
            System.out.println(Thread.currentThread().getName() + "执行了");
        }
    }
}

```





### 3.3 利用Callable接口和Future接口方式实现

```java
package com.study.Test1;

import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class ThreadDemo3 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {

        /*
        *  多线程的第三种实现方式：
        *       特点：可以获取到多线程运行后的结果
        *
        *  1. 创建一个类MyCallable实现Callable接口
        *  2. 重写call方法（返回值表示多线程运行的结果）
        *  3. 创建MyCallable的对象（表示多线程要执行的任务）
        *  4. 创建FutureTask的对象（作用是管理多线程运行的结果）
        *  5. 创建Thread类的对象，并启动（表示多线程）
        * */

        // 创建MyCallable的对象（表示多线程要执行的任务）
        MyCallable mc = new MyCallable();

        // 创建FuturTask的对象（作用管理多线程运行的结果）
        FutureTask<Integer> ft = new FutureTask<>(mc);

        // 创建线程对象
        Thread t1 = new Thread(ft);
        // 启动线程
        t1.start();


        // 获取多线程运行的结果
        Integer result = ft.get();
        System.out.println(result);


    }
}

```





```java
package com.study.Test1;

import java.util.concurrent.Callable;

public class MyCallable implements Callable<Integer> {
    @Override
    public Integer call() throws Exception {
        // 求1~100之间的和
        int sum = 0;
        for (int i = 1; i <= 100; i++) {
            sum += i;
        }
        return sum;
    }
}

```







### 3.4 线程的生命周期

{% asset_img 3.png %}





## 4. 锁

### 4.1 Lock锁

Lock实现提供比使用synchronized方法和语句可以获得更广泛的锁定操作Lock中提供了获得锁和释放锁的方法

- void lock( ): 获得锁
- void unlock( ): 释放锁

Lock是接口不能直接实例化,这里采用它的实现类ReentrantLock来实例化ReentrantLock的构造方法

- ReentrantLock( ): 创建一个ReentrantLock的实例

**Thread方法**

```java
package com.study.aa1;

public class ThreadDemo {
    public static void main(String[] args) {
       /*
           需求：
                某电影院目前正在上映国产大片，共有100张票，而它有3个窗口卖票，请设计一个程序模拟该电影院卖票
       */

        //创建线程对象
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();

        //起名字
        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        //开启线程
        t1.start();
        t2.start();
        t3.start();

    }
}
```



```java
package com.study.aa1;

public class MyThread extends Thread {

    //表示这个类所有的对象，都共享ticket数据
    static int ticket = 0;//0 ~ 99

    @Override
    public void run() {
            while (true) {
                synchronized (MyThread.class) {
                //同步代码块
                if (ticket < 100) {
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    ticket++;
                    System.out.println(getName() + "正在卖第" + ticket + "张票！！！");
                } else {
                    break;
                }
            }
        }
    }

}

```

**Runnable方法**

```java
package com.study.aa2;

public class ThreadDemo {
    public static void main(String[] args) {
       /*
           需求：
                某电影院目前正在上映国产大片，共有100张票，而它有3个窗口卖票，请设计一个程序模拟该电影院卖票
                利用同步方法完成
                技巧：同步代码块
       */

        MyRunnable mr = new MyRunnable();

        Thread t1 = new Thread(mr);
        Thread t2 = new Thread(mr);
        Thread t3 = new Thread(mr);

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        t1.start();
        t2.start();
        t3.start();

    }
}
```



```java
package com.study.aa2;

public class MyRunnable implements Runnable {

    int ticket = 0;

    @Override
    public void run() {
        //1.循环
        while (true) {
            //2.同步代码块（同步方法）
            if (method()) break;
        }
    }

    //this
    private synchronized boolean method() {
        //3.判断共享数据是否到了末尾，如果到了末尾
        if (ticket == 100) {
            return true;
        } else {
            //4.判断共享数据是否到了末尾，如果没有到末尾
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            ticket++;
            System.out.println(Thread.currentThread().getName() + "在卖第" + ticket + "张票！！！");
        }
        return false;
    }
}

```



**Callable方法：**

```java
package com.study.aa3;

public class ThreadDemo {
    public static void main(String[] args) {
       /*
           需求：
                某电影院目前正在上映国产大片，共有100张票，而它有3个窗口卖票，请设计一个程序模拟该电影院卖票
                用JDK5的lock实现
       */

        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        MyThread t3 = new MyThread();

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        t1.start();
        t2.start();
        t3.start();

    }
}
```



```java
package com.study.aa3;

import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class MyThread extends Thread{

    static int ticket = 0;

    static Lock lock = new ReentrantLock();

    @Override
    public void run() {
        //1.循环
        while(true){
            //2.同步代码块
            //synchronized (MyThread.class){
            lock.lock(); //2 //3
            try {
                //3.判断
                if(ticket == 100){
                    break;
                    //4.判断
                }else{
                    Thread.sleep(10);
                    ticket++;
                    System.out.println(getName() + "在卖第" + ticket + "张票！！！");
                }
                //  }
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
            }
        }
    }
}

```







### 4.1 死锁

{% asset_img 5.png %}



```java
package com.study.aa4;


public class ThreadDemo {
    public static void main(String[] args) {
        //  死锁

        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();

        t1.setName("线程A");
        t2.setName("线程B");

        t1.start();
        t2.start();

    }
}
```



```java
package com.study.aa4;

public class MyThread extends Thread {

    static Object objA = new Object();
    static Object objB = new Object();

    @Override
    public void run() {
        //1.循环
        while (true) {
            if ("线程A".equals(getName())) {
                synchronized (objA) {
                    System.out.println("线程A拿到了A锁，准备拿B锁");//A
                    synchronized (objB) {
                        System.out.println("线程A拿到了B锁，顺利执行完一轮");
                    }
                }
            } else if ("线程B".equals(getName())) {
                if ("线程B".equals(getName())) {
                    synchronized (objB) {
                        System.out.println("线程B拿到了B锁，准备拿A锁");//B
                        synchronized (objA) {
                            System.out.println("线程B拿到了A锁，顺利执行完一轮");
                        }
                    }
                }
            }
        }
    }
}
```







## 5. 生产者和消费者

{% asset_img 4.png %}

### 5.1 常见的成员方法

{% asset_img 6.png %}

```java
package com.study.wait_and_notify;
// 消费者
public class Foodie extends Thread {
    public Foodie() {
    }
    /*
     * 1. 循环
     * 2. 同步代码块
     * 3. 判断共享数据是否到了末尾（到了末尾）
     * 4. 判断共享数据是否到了末尾（没有到末尾，执行核心代码）
     * */

    @Override
    public void run() {
        while (true) {
            synchronized (Desk.lock) {
                if (Desk.count == 0) {
                    break;
                } else {
                    // 先判断桌子上是否有面条
                    if (Desk.foodflag == 0) {
                        // 如果没有，就等待
                        try {
                            Desk.lock.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    } else {
                        // 将面条的数量 -1
                        Desk.count--;
                        // 如果有，就开吃
                        System.out.println("吃货开吃面条，还剩" + Desk.count + "碗面条");
                        // 吃完之后唤醒厨师继续做
                        Desk.lock.notifyAll();
                        // 修改桌子的状态
                        Desk.foodflag = 0;
                    }
                }
            }
        }
    }
}
```





```java
package com.study.wait_and_notify;
// 桌子
public class Desk {
    /*
    * 作用：控制生产者和消费者的执行
    *
    * */

    // 是否有面条， 0表示没有面条， 1表示有面条
    public static int foodflag = 0;

    // 面条的总个数
    public static int count = 10;
    
    // 锁的对象
    public static Object lock = new Object();


}

```





```java
package com.study.wait_and_notify;
// 厨师
public class Cook extends Thread {
    public Cook() {
    }
    /*
     * 1. 循环
     * 2. 同步代码块
     * 3. 判断共享数据是否到了末尾（到了末尾）
     * 4. 判断共享数据是否到了末尾（没有到末尾，执行核心代码）
     * */

    @Override
    public void run() {
        while (true) {
            synchronized (Desk.lock) {
                if (Desk.count == 0) {
                    break;
                } else {
                    // 先判断桌子上是否有面条
                    if (Desk.foodflag == 1) {
                        // 如果有面条，就等待
                        try {
                            Desk.lock.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    } else {
                        // 如果没有面条就做面条
                        System.out.println("厨师做了一碗面条！");
                        // 修改桌子上的事物状态
                        Desk.foodflag = 1;
                        // 唤醒吃货吃面条
                        Desk.lock.notifyAll();
                    }
                }
            }
        }
    }
}

```





```java
package com.study.wait_and_notify;
// 主方法
public class ThreadDemo {
    public static void main(String[] args) {

        /*
        * 需求：完成生产者和消费者（等待唤醒机制）的代码
        *      实现线程轮流交替执行的效果
        * */

        // 创建线程的对象
        Cook c = new Cook();
        Foodie f = new Foodie();

        // 给线程设置名字
        c.setName("厨师");
        f.setName("吃货");

        // 开启线程
        c.start();
        f.start();

    }
}

```





******

### 5.2 等待唤醒机制

{% asset_img 7.png %}

```java
package com.study.zs_queue;

import java.util.concurrent.ArrayBlockingQueue;

public class ThreadDemo {
    public static void main(String[] args) {
        /*
         * 需求：利用阻塞队列完成生产者和消费者（等待唤醒机制）的代码
         *      细节：生产者和消费者必须使用同一个阻塞队列
         * */

        // 1. 创建阻塞队列的对象
        ArrayBlockingQueue<String> queue = new ArrayBlockingQueue<>(1);


        // 2. 创建线程的对象，并把阻塞队列传递过去
        Cook c = new Cook(queue);
        Foodie f = new Foodie(queue);

        // 3.开启线程
        c.start();
        f.start();

    }
}

```





```java
package com.study.zs_queue;

import java.util.concurrent.ArrayBlockingQueue;

public class Foodie extends Thread{

    ArrayBlockingQueue<String> queue;

    public Foodie(ArrayBlockingQueue<String> queue) {
        this.queue = queue;
    }

    @Override
    public void run() {
        while(true) {
            // 吃货不断从阻塞队列中获取面条
            try {
                String food = queue.take();
                System.out.println("吃货得到了一碗" + food);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

```





```java
package com.study.zs_queue;

import java.util.concurrent.ArrayBlockingQueue;

public class Cook extends Thread{

    ArrayBlockingQueue<String> queue;

    public Cook(ArrayBlockingQueue<String> queue) {
        this.queue = queue;
    }

    @Override
    public void run() {
        while(true){
            // 不断把面条放入阻塞队列中
            try {
                queue.put("面条");
                System.out.println("厨师做好了一碗面条！");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
    }
}

```





{% asset_img 8.png %}





## 6. 线程池

### 6.1 核心原理

- 创建一个池子，池子中是空的。
- 提交任务时，池子会创建新的线程对象，任务执行完毕，线程归还给池子下回再次提交任务时，不需要创建新的线程，直接复用已有的线程即可。
- 但是如果提交任务时，池子中没有空闲线程，也无法创建新的线程，任务就会排队等待



### 6.2 线程池代码实现

1. 创建线程池
2. 提交任务
3. 所有的任务全部执行完毕，关闭线程池

**线程池的实现方法：**

`public static ExecutorService newFixedThreadPool(int nThreads) ` 创建有上限的线程池



### 6.3 自定义线程池

{% asset_img 9.png %}
