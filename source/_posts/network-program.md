---
title: 网络编程
author: 苦逼小码农
tags:
  - 网络编程
categories:
  - Java
mathjax: true
date: 2023-05-25 21:30:56
---



# 网络编程



## 1.常见的网络架构

### 1.1 客户端/服务器（Client/Server）

用户在本地需要下载并且安装客户端程序，在远程有一个服务器端程序。例如：QQ，Stream...

**特征：**

- 画面精美，用户体验好
- 需要开发客户端和服务端
- 用户需要下载和更新客户端

- 适合开发互联网应用，可以随时随地访问





### 1.2 浏览器/服务器（Browser/Server）

只需要有一个浏览器，用户通过不同的网址，客户访问不同的服务器。例如：淘宝，百度

**特征：**

- 不需要开发客户端，只需要开发服务端
- 用户不需要下载，打开浏览器就能用
- 如果应用过大，数据过多的话，用户体验会受影响

- 适合开发办公类及其大型游戏，稳定，体验好

{% asset_img 1.png %}



## 2. 网络编程三要素

### 2.1 IP地址

设备在网络中的地址，识别该设备的唯一标识



#### 2.1.1  IPV4

采用32位地址长度，分成4组，共有个IP地址，IPV4共有2^32个IP地址（约有43亿）。

{% asset_img 2.png %}

**IPV4的地址分类形式**

- 公网地址(万维网使用)和私有地址(局域网使用)。
- 192.168.开头的就是私有址址，范围即为192.168.0.0--192.168.255.255，专门为组织机构内部使用，以此节省IP



#### 2.1.2  IPV6

采用128位地址长度，分成8组，可以给地球上的每一粒沙子分配一个IP地址。

{% asset_img 3.png %}





#### 2.1.3 常用的CMD命令

- ipconfig：查看本机IP地址

- ping：检查网络是否连通

{% asset_img 4.png %}



> 特殊IP地址：127.0.0.1 <==> localhost (本机IP地址)



#### 2.1.4  获取IP地址的方法

- `static InetAddress getByName(String host)`确定主机名的IP地址，主机名可以是机器名称，也可以是IP地址
- `String getHostName() `获取IP地址的主机名
- `String getHostAddress()`返回文本显示中的IP地址字符串

```java
package com.study.a01;

import java.net.InetAddress;
import java.net.UnknownHostException;

public class Test {
    public static void main(String[] args) throws UnknownHostException {
        /*
        * static InetAddress getByName(String host) 确定主机名的IP地址，主机名可以是机器名称，也可以是IP地址
        * String getHostName()                      获取IP地址的主机名
        * String getHostAddress()                   返回文本显示中的IP地址字符串
        * */

        // 1.获取InetAddress的对象
        InetAddress address = InetAddress.getByName("Spicy-pig");
        System.out.println(address);

        // 2.获取IP地址的主机名
        String name = address.getHostName();
        System.out.println(name);// Spicy-pig

        // 3.返回文本显示中的IP地址字符串
        String ip = address.getHostAddress();
        System.out.println(ip);// 10.30.185.145
    }
}

```





### 2.2 端口号

应用程序在设备中的唯一标识。

端口号:由两个字节表示的整数，取值范围:0—65535。

其中0—1023之间的端口号用于一些知名的网络服务或者应用。我们自己使用1024以上的端口号就可以了。

{% asset_img 5.png %}



### 2.3 协议

数据在网络中传输的规则，常见的协议有UDP，TCP，HTTP，HTTPS，FTP。

{% asset_img 6.png %}



#### 2.3.1 UDP协议

- 用户数据报协议(User Datagram Protocol)
- UDP是面向无连接通信协议。
- 速度快，有大小限制一次最多发送64K，数据不安全，易丢失数据。

{% asset_img 7.png %}





#### 2.3.2 TCP协议

- 传输控制协议TCP(Transmission Control Protocol)
- TCP协议是面向连接的通信协议。
- 速度慢，没有大小限制，数据安全。

{% asset_img 8.png %}



#### 2.3.3 数据的收发步骤



**接收数据的一般步骤：**

- 创建发送端DatagramSocket的对象
- 打包数据
- 发送数据
- 释放资源

```java
package com.study.a02;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class Receive {
    public static void main(String[] args) throws IOException {
        // 接受数据

        // 1. 创建DatagramSocket对象（快递公司）
        // 细节：
        //      再接收的时候一定要绑定端口
        //      绑定的端口一定要和发送的端口一样
        DatagramSocket ds = new DatagramSocket(10086);

        // 2.接收数据包
        byte[] bytes = new byte[1024];
        DatagramPacket dp = new DatagramPacket(bytes, bytes.length);

        // 该方法是阻塞的
        // 程序执行到这里时，如果下面的receive语句没有执行的话就会发生阻塞
        System.out.println("请求已发送！");
        ds.receive(dp);
        System.out.println("已收到回复！");

        // 3.解析数据包
        byte[] data = dp.getData();
        int len = dp.getLength();
        InetAddress address = dp.getAddress();
        int port = dp.getPort();

        System.out.println("接收到的数据为：" + new String(data, 0, len));
        System.out.println("该数据是从 " + address + " 这台电脑的 " + port + " 这个端口发出的");

    }
}


```



**发送数据的一般步骤：**

- 创建接收端DatagramSocket的对象
- 接收打包好的数据
- 解析数据包
- 释放资源

```java
package com.study.a02;

import java.io.IOException;
import java.net.*;

public class Send {
    public static void main(String[] args) throws IOException {
        // 发送数据

        // 1.创建DatagramSocket对象(快递公司)
        //   细节:
        // 绑定端口，以后我们就是通过这个端口往外发送
        // 空参:所有可用的端口中随机一个进行使用
        // 有参:指定端口号进行绑定
        DatagramSocket ds = new DatagramSocket();


        // 2.打包数据
        String str = "Hello， 你好啊！";
        byte[] bytes = str.getBytes();
        InetAddress address = InetAddress.getByName("127.0.0.1");
        int port = 10086;

        DatagramPacket dp = new DatagramPacket(bytes, bytes.length, address, port);

        // 3.发送数据
        ds.send(dp);

        // 4.释放资源
        ds.close();


    }

}

```





## 3. UDP通信程序

### 3.1 UDP发送数据

- 找到快递公司（创建发送端的DatagramSocket对象）
- 打包快递（打包数据DatagramPacket）
- 快递公司发送包裹（发送数据）
- 付钱走人（释放资源）

```java
package com.study.a03udp;

import java.io.IOException;
import java.net.*;
import java.util.Scanner;

public class Send {
    public static void main(String[] args) throws IOException {
         /*
            按照下面的要求实现程序
                UDP发送数据：数据来自于键盘录入，直到输入的数据是886，发送数据结束
                UDP接收数据：因为接收端不知道发送端什么时候停止发送，故采用死循环接收
        */

        //1.创建对象DatagramSocket的对象
        DatagramSocket ds = new DatagramSocket();

        //2.打包数据
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("请输入您要说的话：");
            String str = sc.nextLine();
            if("886".equals(str)){
                break;
            }
            byte[] bytes = str.getBytes();
            InetAddress address = InetAddress.getByName("127.0.0.1");
            int port = 10086;
            DatagramPacket dp = new DatagramPacket(bytes,bytes.length,address,port);

            //3.发送数据
            ds.send(dp);
        }

        //4.释放资源
        ds.close();

    }
}


```



### 3.2 UDP接收数据

- 找快递公司（创建接收端的DatagramSocket对象）
- 取快递（接收打包好的数据）
- 拆分快递（解析数据包）
- 签收走人（释放资源）

```java
package com.study.a03udp;

import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class Receive {
    public static void main(String[] args) throws IOException {
        // 接收数据
        /*
         * 需求：
         *      UDP发送数据：数据来源于键盘录入，直到数据为886是结束聊天
         *      UDP接收数据：因为接收端不知道发送端是什么时候停止发送，故采用死循环接受
         * */
        // 1.创建DatagramSocket的对象（快递公司）
        DatagramSocket ds = new DatagramSocket(10086);

        // 2.接收数据包
        byte[] bytes = new byte[1024];
        DatagramPacket dp = new DatagramPacket(bytes, bytes.length);

        while (true) {
            ds.receive(dp);

            // 3.解析数据包
            byte[] data = dp.getData();
            int len = dp.getLength();
            String ip = dp.getAddress().getHostAddress();
            String name = dp.getAddress().getHostName();

            // 4.打印数据包
            System.out.println("ip为" + ip + ", 主机名为" + name + "的电脑，发送了数据：" + new String(data, 0, len));

        }

    }

}

```







## 4. TCP通信程序

{% asset_img 9.png %}

### 4.1 TCP发送数据

- 创建客户端的Socket对象与指定服务器连接
  - Socket ( String host, int port )
- 获取输出流，写数据 
  - OutputStream getOutputStream( )
- 释放资源
  - close( ) (无返回值)

```java
package com.study.a04tcp;

import java.io.IOException;
import java.io.OutputStream;
import java.net.Socket;

public class Client {
    public static void main(String[] args) throws IOException {
        // TCP协议，发送数据

        // 1.创建Socket对象
        // 细节:在创建对象的同时会连接服务端
        //      如果连接不上，代码会报错
        Socket socket = new Socket("127.0.0.1", 10000);


        // 2.可以从连接通道中获取输出流
        OutputStream os = socket.getOutputStream();
        // 写出数据
        os.write("泰裤辣".getBytes());

        // 3.释放资源
        os.close();
        socket.close();


    }
}

```







### 4.2 TCP接收数据

- 创建服务端的Socket对象ServerSocket
  - ServerSocket  ( int port )
- 监听客户端连接，返回一个Socket对象
  - Socket accept ( )
- 获取输入流，读数据，并把数据显示在控制台
  - InputStream( ) getInputStream( )
- 释放资源
  - close( ) (无返回值)

```java
package com.study.a04tcp;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class Server {
    public static void main(String[] args) throws IOException {
        // TCP协议，接收数据

        // 1.创建对象SocketServer
        ServerSocket ss = new ServerSocket(10000);

        // 2.监听客户端的连接
        Socket socket = ss.accept();

        // 3.从连接通道中获取输出流读取数据
/*      InputStream is = socket.getInputStream();
        InputStreamReader isr = new InputStreamReader(is);
        BufferedReader br = new BufferedReader(isr);
        */

        BufferedReader br = new BufferedReader(new InputStreamReader(socket.getInputStream()));

        int b;
        while((b = br.read()) != -1){
            System.out.print((char) b);
        }

        // 4.释放资源
        socket.close();
        ss.close();

    }
}

```





