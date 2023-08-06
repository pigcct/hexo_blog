---
title: 基于Java Swing图书管理系统
author: 苦逼小码农
tags:
  - Swing
categories:
  - Java
mathjax: true
date: 2023-07-03 23:30:39
---





## 1. 项目概述



### 1.1 项目结构：

- 用户注册

- 用户登录

- 用户管理员操作界面



**用户**



{% asset_img 1.png %}







**管理员**

{% asset_img 2.png %}



### 1.2 E—R图

**user**

{% asset_img 3.png %}



**book**

{% asset_img 4.png %}



**book_type**

{% asset_img 5.png %}





**borrowdetail**

{% asset_img 6.png %}







## 2. 项目环境搭建



### 2.1 确定项目开发环境

**操作系统：window 10**

**Java开发包：jdk18**

**数据库：mysql 8.0(Navicate)**

**开发工具：IntelliJ IDEA 2022.2.2**



### 2.2 创建数据库



在Navicat中连接MySQL数据库后新建数据库mybookmanager，并在该数据库中建立相应的表



### 2.3 引入jar包

{% asset_img 11.png %}





### 2.4 创建包目录结构

{% asset_img 12.png %}

- dao包下的java文件为与数据库进行交互的类
- Jframe包下的java文件为UI界面
- model包下的java文件为实体类
- utils包中的类为项目中所用到的工具类





## 3. 数据库设计



**数据库名：mybookmanager**

**字符集：utf-8**

**端口号：3306**



**user**

{% asset_img 7.png %}



**book**

{% asset_img 8.png %}



**book_type**

{% asset_img 9.png %}



**borrowdetail**

{% asset_img 10.png %}



**建表以及插入语句**

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : Java
 Source Server Type    : MySQL
 Source Server Version : 80026 (8.0.26)
 Source Host           : localhost:3306
 Source Schema         : bookmanager

 Target Server Type    : MySQL
 Target Server Version : 80026 (8.0.26)
 File Encoding         : 65001

 Date: 04/07/2023 12:34:07
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for book
-- ----------------------------
DROP TABLE IF EXISTS `book`;
CREATE TABLE `book`  (
  `id` int NOT NULL AUTO_INCREMENT,
  `book_name` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `tyPE_id` int NULL DEFAULT NULL,
  `author` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `publish` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `PRice` double(10, 2) NULL DEFAULT NULL,
  `number` int NULL DEFAULT NULL,
  `status` int NULL DEFAULT 1 COMMENT '状态 1上架0下架',
  `remark` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 17 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = COMPACT;

-- ----------------------------
-- Records of book
-- ----------------------------
INSERT INTO `book` VALUES (1, 'Java核心技术', 1, '霍斯特曼', '人民邮电出版社', 69.00, 16, 1, 'Java基础教学');
INSERT INTO `book` VALUES (2, 'Tomcat与Java web', 1, '孙卫琴', '人民邮电出版社', 119.00, 16, 1, 'javaweb教学');
INSERT INTO `book` VALUES (3, ';mySQL基础教程', 1, '西泽梦路', '人民邮电出版社', 129.00, 16, 1, 'MySQL基础教学');
INSERT INTO `book` VALUES (4, '西游记', 3, '吴承恩', '机械工业出版社', 23.00, 213, 1, '四大名著之一');
INSERT INTO `book` VALUES (6, 'SpringCloud微服务架构开发', 1, '黑马程序员', '人民邮电出版社', 28.00, 20, 1, '微服务实战开发');
INSERT INTO `book` VALUES (7, '水浒传', 3, '施耐庵 ', '人民文学出版社', 29.00, 30, 1, '四大名著之一');
INSERT INTO `book` VALUES (16, 'jspringboot', 4, 'cc', 'xx', 5.20, 1000, 1, 'springboot');

-- ----------------------------
-- Table structure for book_type
-- ----------------------------
DROP TABLE IF EXISTS `book_type`;
CREATE TABLE `book_type`  (
  `id` int NOT NULL AUTO_INCREMENT,
  `type_name` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `remark` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 5 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = COMPACT;

-- ----------------------------
-- Records of book_type
-- ----------------------------
INSERT INTO `book_type` VALUES (1, '技术', '技术hhh');
INSERT INTO `book_type` VALUES (2, '人文', '人文类');
INSERT INTO `book_type` VALUES (3, '小说', '人生情感小说');
INSERT INTO `book_type` VALUES (4, '科技类', '科技类');

-- ----------------------------
-- Table structure for borrowdetail
-- ----------------------------
DROP TABLE IF EXISTS `borrowdetail`;
CREATE TABLE `borrowdetail`  (
  `id` int NOT NULL AUTO_INCREMENT,
  `user_id` int NOT NULL,
  `book_id` int NOT NULL,
  `status` int NOT NULL COMMENT '状态  1在借2已还',
  `borrow_time` bigint NULL DEFAULT NULL,
  `return_time` bigint NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 30 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = COMPACT;

-- ----------------------------
-- Records of borrowdetail
-- ----------------------------
INSERT INTO `borrowdetail` VALUES (1, 1, 2, 2, 1546414916391, 1546414948498);
INSERT INTO `borrowdetail` VALUES (2, 1, 3, 2, 1546414932877, 1556417443285);
INSERT INTO `borrowdetail` VALUES (3, 1, 2, 2, 1546416530026, 1546416640210);
INSERT INTO `borrowdetail` VALUES (4, 1, 1, 2, 1546565100120, 1556334334816);
INSERT INTO `borrowdetail` VALUES (5, 1, 4, 2, 1546565102870, 1688392384101);
INSERT INTO `borrowdetail` VALUES (6, 3, 1, 2, 1546565519776, 1556207839074);
INSERT INTO `borrowdetail` VALUES (7, 3, 4, 1, 1546565522374, NULL);
INSERT INTO `borrowdetail` VALUES (8, 1, 1, 2, 1556427836809, 1688392380686);
INSERT INTO `borrowdetail` VALUES (9, 4, 3, 1, 1556433544156, NULL);
INSERT INTO `borrowdetail` VALUES (10, 7, 5, 1, 1556503388763, NULL);
INSERT INTO `borrowdetail` VALUES (11, 8, 5, 2, 1556507260569, 1556507349243);
INSERT INTO `borrowdetail` VALUES (27, 1, 6, 1, 1688389422921, NULL);
INSERT INTO `borrowdetail` VALUES (28, 1, 4, 1, 1688429793391, NULL);
INSERT INTO `borrowdetail` VALUES (29, 1, 2, 1, 1688445082661, NULL);

-- ----------------------------
-- Table structure for user
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user`  (
  `id` int NOT NULL AUTO_INCREMENT,
  `username` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `password` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `role` int NULL DEFAULT NULL COMMENT '角色  1学生 2管理员',
  `sex` varchar(1) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  `phone` char(11) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 17 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = COMPACT;

-- ----------------------------
-- Records of user
-- ----------------------------
INSERT INTO `user` VALUES (1, 'xx', '111111', 1, '男', '13195648799');
INSERT INTO `user` VALUES (2, 'admin', '111111', 2, '男', '13198645975');
INSERT INTO `user` VALUES (3, '徐某人', 'xkj123', 1, '女', '13195648529');
INSERT INTO `user` VALUES (4, '肖淼', 'sDF78978', 1, '女', '13195698458');
INSERT INTO `user` VALUES (12, '1111', '1111yyyy', 1, '男', '15076281789');
INSERT INTO `user` VALUES (13, '11', '15076281789yy', 1, '男', '15076281789');
INSERT INTO `user` VALUES (14, '222', '15076281789yy', 1, '男', '15076281789');
INSERT INTO `user` VALUES (15, 'xxn', '12345yyy', 1, '男', '15076281789');
INSERT INTO `user` VALUES (16, 'xxx', '12345678yy', 2, '男', '15076281789');

SET FOREIGN_KEY_CHECKS = 1;

```







## 4. 实体类设计(model)

### 4.1 User



```java
package com.hechaodong.bookmanager.model;

// 用户类
public class User {
	private Integer userId;  // 用户id
	private String userName; // 用户名
	private String password; // 密码
	private Integer role;	 //用户角色  1普通  2管理员
	private String sex;		// 用户性别
	private String phone;   // 用户手机号

	/**
	 * 获取
	 * @return userId
	 */
	public Integer getUserId() {
		return userId;
	}

	/**
	 * 设置
	 * @param userId
	 */
	public void setUserId(Integer userId) {
		this.userId = userId;
	}

	/**
	 * 获取
	 * @return userName
	 */
	public String getUserName() {
		return userName;
	}

	/**
	 * 设置
	 * @param userName
	 */
	public void setUserName(String userName) {
		this.userName = userName;
	}

	/**
	 * 获取
	 * @return password
	 */
	public String getPassword() {
		return password;
	}

	/**
	 * 设置
	 * @param password
	 */
	public void setPassword(String password) {
		this.password = password;
	}

	/**
	 * 获取
	 * @return role
	 */
	public Integer getRole() {
		return role;
	}

	/**
	 * 设置
	 * @param role
	 */
	public void setRole(Integer role) {
		this.role = role;
	}

	/**
	 * 获取
	 * @return sex
	 */
	public String getSex() {
		return sex;
	}

	/**
	 * 设置
	 * @param sex
	 */
	public void setSex(String sex) {
		this.sex = sex;
	}

	/**
	 * 获取
	 * @return phone
	 */
	public String getPhone() {
		return phone;
	}

	/**
	 * 设置
	 * @param phone
	 */
	public void setPhone(String phone) {
		this.phone = phone;
	}

	public String toString() {
		return "User{userId = " + userId +
				", userName = " + userName +
				", password = " + password +
				", role = " + role +
				", sex = " + sex +
				", phone = " + phone +
				"}";
	}
}

```



### 4.2 Book



```java
package com.hechaodong.bookmanager.model;

// 图书类
public class Book {
	private Integer bookId;
	private String bookName;
	private String author;
	private Integer status;//状态 1上架  2下架
	private Integer bookTypeId;
	private String publish;
	private Integer number;// 库存数量
	private double price;
	private String remark;

	/**
	 * 获取
	 * @return bookId
	 */
	public Integer getBookId() {
		return bookId;
	}

	/**
	 * 设置
	 * @param bookId
	 */
	public void setBookId(Integer bookId) {
		this.bookId = bookId;
	}

	/**
	 * 获取
	 * @return bookName
	 */
	public String getBookName() {
		return bookName;
	}

	/**
	 * 设置
	 * @param bookName
	 */
	public void setBookName(String bookName) {
		this.bookName = bookName;
	}

	/**
	 * 获取
	 * @return author
	 */
	public String getAuthor() {
		return author;
	}

	/**
	 * 设置
	 * @param author
	 */
	public void setAuthor(String author) {
		this.author = author;
	}

	/**
	 * 获取
	 * @return status
	 */
	public Integer getStatus() {
		return status;
	}

	/**
	 * 设置
	 * @param status
	 */
	public void setStatus(Integer status) {
		this.status = status;
	}

	/**
	 * 获取
	 * @return bookTypeId
	 */
	public Integer getBookTypeId() {
		return bookTypeId;
	}

	/**
	 * 设置
	 * @param bookTypeId
	 */
	public void setBookTypeId(Integer bookTypeId) {
		this.bookTypeId = bookTypeId;
	}

	/**
	 * 获取
	 * @return publish
	 */
	public String getPublish() {
		return publish;
	}

	/**
	 * 设置
	 * @param publish
	 */
	public void setPublish(String publish) {
		this.publish = publish;
	}

	/**
	 * 获取
	 * @return number
	 */
	public Integer getNumber() {
		return number;
	}

	/**
	 * 设置
	 * @param number
	 */
	public void setNumber(Integer number) {
		this.number = number;
	}

	/**
	 * 获取
	 * @return price
	 */
	public double getPrice() {
		return price;
	}

	/**
	 * 设置
	 * @param price
	 */
	public void setPrice(double price) {
		this.price = price;
	}

	/**
	 * 获取
	 * @return remark
	 */
	public String getRemark() {
		return remark;
	}

	/**
	 * 设置
	 * @param remark
	 */
	public void setRemark(String remark) {
		this.remark = remark;
	}

	public String toString() {
		return "Book{bookId = " + bookId +
				", bookName = " + bookName +
				", author = " + author +
				", status = " + status +
				", bookTypeId = " + bookTypeId +
				", publish = " + publish +
				", number = " + number +
				", price = " + price +
				", remark = " + remark +
				"}";
	}
}

```





### 4.3 BookType



```java
package com.hechaodong.bookmanager.model;


// 图书类型
public class BookType {
	private Integer typeId;
	private String typeName;
	private String remark;

	/**
	 * 获取
	 * @return typeId
	 */
	public Integer getTypeId() {
		return typeId;
	}

	/**
	 * 设置
	 * @param typeId
	 */
	public void setTypeId(Integer typeId) {
		this.typeId = typeId;
	}

	/**
	 * 获取
	 * @return typeName
	 */
	public String getTypeName() {
		return typeName;
	}

	/**
	 * 设置
	 * @param typeName
	 */
	public void setTypeName(String typeName) {
		this.typeName = typeName;
	}

	/**
	 * 获取
	 * @return remark
	 */
	public String getRemark() {
		return remark;
	}

	/**
	 * 设置
	 * @param remark
	 */
	public void setRemark(String remark) {
		this.remark = remark;
	}

	public String toString() {
		return "BookType{typeId = " + typeId +
				", typeName = " + typeName +
				", remark = " + remark +
				"}";
	}
}

```





### 4.4 BorrowDetail



```java
package com.hechaodong.bookmanager.model;

// 借阅信息
public class BorrowDetail {
	private Integer borrowId;
	private Integer userId;
	private Integer bookId;
	private Integer status;//状态  1在借  2已还
	private Long borrowTime;
	private Long returnTime;

	/**
	 * 获取
	 * @return borrowId
	 */
	public Integer getBorrowId() {
		return borrowId;
	}

	/**
	 * 设置
	 * @param borrowId
	 */
	public void setBorrowId(Integer borrowId) {
		this.borrowId = borrowId;
	}

	/**
	 * 获取
	 * @return userId
	 */
	public Integer getUserId() {
		return userId;
	}

	/**
	 * 设置
	 * @param userId
	 */
	public void setUserId(Integer userId) {
		this.userId = userId;
	}

	/**
	 * 获取
	 * @return bookId
	 */
	public Integer getBookId() {
		return bookId;
	}

	/**
	 * 设置
	 * @param bookId
	 */
	public void setBookId(Integer bookId) {
		this.bookId = bookId;
	}

	/**
	 * 获取
	 * @return status
	 */
	public Integer getStatus() {
		return status;
	}

	/**
	 * 设置
	 * @param status
	 */
	public void setStatus(Integer status) {
		this.status = status;
	}

	/**
	 * 获取
	 * @return borrowTime
	 */
	public Long getBorrowTime() {
		return borrowTime;
	}

	/**
	 * 设置
	 * @param borrowTime
	 */
	public void setBorrowTime(Long borrowTime) {
		this.borrowTime = borrowTime;
	}

	/**
	 * 获取
	 * @return returnTime
	 */
	public Long getReturnTime() {
		return returnTime;
	}

	/**
	 * 设置
	 * @param returnTime
	 */
	public void setReturnTime(Long returnTime) {
		this.returnTime = returnTime;
	}

	public String toString() {
		return "BorrowDetail{borrowId = " + borrowId +
				", userId = " + userId +
				", bookId = " + bookId +
				", status = " + status +
				", borrowTime = " + borrowTime +
				", returnTime = " + returnTime +
				"}";
	}
}

```









## 5. 工具类设计(utils)



### 5.1 DdUtil



```java
package com.hechaodong.bookmanager.utils;

import java.sql.*;

public class DbUtil {
	// 定义数据库连接字符串
	private String Driver = "com.mysql.cj.jdbc.Driver";	// 数据库驱动
	private String Url = "jdbc:mysql://localhost:3306/mybookmanager?serverTimezone=UTC&useSSL=false";
	private String UserName = "root";
	private String Password = "******";

	// 连接数据库
	public Connection getConnection()throws Exception{
	    Class.forName(Driver);
		Connection con = (Connection) DriverManager.getConnection(Url,UserName,Password);
		return con;
	}

	// 关闭数据库
	public void closeCon (Connection con)throws Exception {
		if(con!=null){
			con.close();
		}
	}

}

```





### 5.2 ToolUtil



```java
package com.hechaodong.bookmanager.utils;

import java.text.SimpleDateFormat;
import java.util.Date;
import javax.servlet.http.HttpSession;

import com.hechaodong.bookmanager.model.User;

public class ToolUtil {
	//判断一个字符串是否为空，如果不为空则返回false，空字符串或者null返回true
	public static boolean isEmpty(String str){
		if(str != null && !"".equals(str.trim())){
			return false;
		}
		return true;
	}

	//获取当前时间的时间戳，以毫秒为单位
	public static Long getTime(){
		long time = System.currentTimeMillis();
		return time;
	}

	//将给定的时间戳转换为对应的日期时间字符串，格式为"yyyy-MM-dd HH:mm:ss"
	public static String getDateByTime(Long time){
		SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		String string = format.format(new Date(time));
		return string;
	}

	//从给定的HttpSession对象中获取保存的当前用户对象(User)
	public static User getUser(HttpSession session){
		User user = (User) session.getAttribute("user");
		return user;
	}

	//将给定的当前用户对象(User)存储到HttpSession对象中，以便在会话期间使用
	public static void setUser(HttpSession session,User user){
		session.setAttribute("user", user);
	}
}

```











## 6. 数据库交互类设计(dao)



### 6.1 UserDao



```java
package com.hechaodong.bookmanager.dao;

import java.sql.*;
import com.hechaodong.bookmanager.model.User;
import com.hechaodong.bookmanager.utils.ToolUtil;

import java.sql.ResultSet;
public class UserDao {
	
	public User login(Connection con, User user)throws Exception {

		// 定义一个User类型的变量，用来记录查询的结果
		User resultUser = null;

		// 定义sql语句
		String sql = "select * from user where username=? and password=? and role = ?";
	    PreparedStatement preparedStatement = (PreparedStatement) con.prepareStatement(sql);
		preparedStatement.setString(1,user.getUserName());
		preparedStatement.setString(2,user.getPassword());
		preparedStatement.setInt(3,user.getRole());

		// 执行查询操作
	    ResultSet rs = preparedStatement.executeQuery();
	    if(rs.next()){
	    	resultUser = new User();
	    	resultUser.setUserId(rs.getInt("id"));
	    	resultUser.setUserName(rs.getString("username"));
	    	resultUser.setSex(rs.getString("sex"));
	    	resultUser.setPhone(rs.getString("phone"));
	    }
		return resultUser;
	}

	// 添加用户信息
	public int addUser(Connection con, User user) throws Exception{
		//查询注册用户名是否存在
		String sql = "select * from user where userName=? ";
	    PreparedStatement pstmt = (PreparedStatement) con.prepareStatement(sql);
		pstmt.setString(1,user.getUserName());
	    ResultSet rs = pstmt.executeQuery();
	    if(rs.next()){
	    	return 2;
	    }

		// 执行插入操作
	    String sql2="insert into user (username,password,role,sex,phone) values (?,?,?,?,?)";
	    PreparedStatement pstmt2=(PreparedStatement) con.prepareStatement(sql2);
		pstmt2.setString(1, user.getUserName());
		pstmt2.setString(2, user.getPassword());
		pstmt2.setInt(3, user.getRole());
		pstmt2.setString(4,user.getSex());
		pstmt2.setString(5,user.getPhone());

		return pstmt2.executeUpdate();
	}
	

	// 查询用户信息
	public ResultSet list(Connection con,User user)throws Exception{
		StringBuffer sb=new StringBuffer("select * from user where role = 1");
		if(!ToolUtil.isEmpty(user.getUserName())){
			sb.append(" and username like '%"+user.getUserName()+"%'");
		}
		PreparedStatement pstmt=(PreparedStatement) con.prepareStatement(sb.toString());

		return pstmt.executeQuery();
	}

	// 更新信息
	public int update(Connection con,User user)throws Exception{
		String sql="update user set username=?,password=?,sex=?,phone=? where id=?";
		PreparedStatement pstmt=(PreparedStatement) con.prepareStatement(sql);
		pstmt.setString(1, user.getUserName());
		pstmt.setString(2, user.getPassword());
		pstmt.setString(3, user.getSex());
		pstmt.setString(4, user.getPhone());
		pstmt.setInt(5, user.getUserId());

		return pstmt.executeUpdate();
	}
}

```



### 6.2 BookDao

```java
package com.hechaodong.bookmanager.dao;

import java.sql.*;
import java.sql.ResultSet;

import com.hechaodong.bookmanager.model.Book;
import com.hechaodong.bookmanager.utils.ToolUtil;

// 图书信息的增删改查操作
public class BookDao {

    // 图书添加
    public int add(Connection con, Book book) throws Exception {
        String sql = "insert into book (book_name,type_id,author,publish,price,number,status,remark) values(?,?,?,?,?,?,?,?)";
        PreparedStatement preparedStatement = (PreparedStatement) con.prepareStatement(sql);
        preparedStatement.setString(1, book.getBookName());// 以getBookName()第一个参数添加到sql语句的第一个占位符中
        preparedStatement.setInt(2, book.getBookTypeId());
        preparedStatement.setString(3, book.getAuthor());
        preparedStatement.setString(4, book.getPublish());
        preparedStatement.setDouble(5, book.getPrice());
        preparedStatement.setInt(6, book.getNumber());
        preparedStatement.setInt(7, book.getStatus());
        preparedStatement.setString(8, book.getRemark());

        return preparedStatement.executeUpdate();
    }


    // 查询图书信息
    public ResultSet list(Connection con, Book book) throws Exception {
        // 创建StringBuffer对象，来拼接sql语句
        StringBuffer sb = new StringBuffer("select b.*,bt.type_name from book b,book_type bt where b.type_id=bt.id");
        if (!ToolUtil.isEmpty(book.getBookName())) {
            sb.append(" and b.book_name like '%" + book.getBookName() + "%'");
        }
        if (!ToolUtil.isEmpty(book.getAuthor())) {
            sb.append(" and b.author like '%" + book.getAuthor() + "%'");
        }
        if (book.getBookTypeId() != null && book.getBookTypeId() != 0) {
            sb.append(" and b.type_id=" + book.getBookTypeId());
        }
        if (book.getStatus() != null) {
            sb.append(" and b.status=" + book.getStatus());
        }
        if (book.getBookId() != null) {
            sb.append(" and b.id=" + book.getBookId());
        }
        sb.append(" ORDER BY b.status");
        PreparedStatement preparedStatement = (PreparedStatement) con.prepareStatement(sb.toString());

        return preparedStatement.executeQuery();

    }

    // 查询可借阅的图书信息
    public ResultSet listCan(Connection con, Book book) throws Exception {
        StringBuffer sb = new StringBuffer("select b.*,bt.type_name from book b,book_type bt where type_id=bt.id and b.status = 1");
        // 字符串的拼接查询
        if (!ToolUtil.isEmpty(book.getBookName())) {
            sb.append(" and b.book_name like '%" + book.getBookName() + "%'");
        }
        if (book.getBookId() != null) {
            sb.append(" and b.id=" + book.getBookId());
        }
        PreparedStatement preparedStatement = (PreparedStatement) con.prepareStatement(sb.toString());

        return preparedStatement.executeQuery();
    }


    // 图书信息删除
    public int delete(Connection con, String id) throws Exception {
        String sql = "delete from book where id=?";
        PreparedStatement preparedStatement = (PreparedStatement) con.prepareStatement(sql);
        preparedStatement.setString(1, id);

        return preparedStatement.executeUpdate();
    }

    // 图书信息修改
    public int update(Connection con, Book book) throws Exception {
        String sql = "update book set book_name=?,type_id=?,author=?,publish=?,price=?,number=?,status=?,remark=? where id=?";
        PreparedStatement statement = con.prepareStatement(sql);
        statement.setString(1, book.getBookName());
        statement.setInt(2, book.getBookTypeId());
        statement.setString(3, book.getAuthor());
        statement.setString(4, book.getPublish());
        statement.setDouble(5, book.getPrice());
        statement.setInt(6, book.getNumber());
        statement.setInt(7, book.getStatus());
        statement.setString(8, book.getRemark());
        statement.setInt(9, book.getBookId());

        return statement.executeUpdate();
    }

}

```



### 6.3 BookTypeDao

```java
package com.hechaodong.bookmanager.dao;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

import com.hechaodong.bookmanager.model.BookType;
import com.hechaodong.bookmanager.utils.ToolUtil;

public class BookTypeDao {
	
	// 图书类别添加
	public int add(Connection con,BookType bookType)throws Exception{
		// 先查询是否有一样的类别名
		String sql="select * from book_type where type_name = ?";
		PreparedStatement preparedStatement=con.prepareStatement(sql);
		preparedStatement.setString(1, bookType.getTypeName());
		ResultSet resultSet = preparedStatement.executeQuery();
		while(resultSet.next()){
			/*
			* 遍历结果集
			* 如果结果集中有记录，则表示已存在相同名称的图书类型，那么立即返回数字 2，表示添加失败
			* */
			return 2;
		}

		// 完成类别数据的插入操作
		sql="insert into book_type (type_name,remark) values(?,?)";
		PreparedStatement statement=con.prepareStatement(sql);
		statement.setString(1, bookType.getTypeName());
		statement.setString(2, bookType.getRemark());

		return statement.executeUpdate();
	}

	// 查询图书类别集合
	public ResultSet list(Connection con,BookType bookType)throws Exception{
		StringBuffer sb=new StringBuffer("select * from book_type");
		// 判断传入的图书类型对象 bookType 的名称是否为空
		if(!ToolUtil.isEmpty(bookType.getTypeName())){
			sb.append(" and type_name like '%"+bookType.getTypeName()+"%'");
		}
		PreparedStatement preparedStatement=con.prepareStatement(sb.toString().replaceFirst("and", "where"));

		return preparedStatement.executeQuery();
	}
	
	// 删除图书类别
	public int delete(Connection con,String id)throws Exception{
		//先查询该类别下是否有书籍
		String sql="select b.* from book b left join book_type bt on b.type_id = bt.id where bt.id =? ";
		PreparedStatement preparedStatement=con.prepareStatement(sql);
		preparedStatement.setString(1, id);
		ResultSet query = preparedStatement.executeQuery();// 查询操作
		int number =0;
		while(query.next()){
			number++;
		}
		if(number > 0){ // 表示该类别下存在书籍，那么立即返回数字 3，表示删除失败
			return 3;
		}
		
		//判断类别总数是否大于1
		sql="select * from book_type";
		PreparedStatement pstmt2=con.prepareStatement(sql);
		ResultSet resultSet = pstmt2.executeQuery();
		int count = 0;
		while(resultSet.next()){
			count++;
		}
		if(count<2){ // 如果计数器 count 的值小于 2，表示图书类型的总数小于 2，即只有一个类别，那么立即返回数字 2，表示删除失败
			return 2;
		}
		sql="delete from book_type where id=?";
		PreparedStatement pstmt3=con.prepareStatement(sql);
		pstmt3.setString(1, id);

		return pstmt3.executeUpdate();
	}
	
	// 更新图示类别
	public int update(Connection con,BookType bookType)throws Exception{
		String sql="update book_type set type_name=?,remark=? where id=?";
		PreparedStatement pstmt=con.prepareStatement(sql);
		pstmt.setString(1, bookType.getTypeName());
		pstmt.setString(2, bookType.getRemark());
		pstmt.setInt(3, bookType.getTypeId());

		return pstmt.executeUpdate();
	}
}

```



### 6.4 BorrowDetailDao



```java
package com.hechaodong.bookmanager.dao;

import java.sql.*;
import java.sql.ResultSet;
import com.hechaodong.bookmanager.model.BorrowDetail;

public class BorrowDetailDao {

	public ResultSet list(Connection con,BorrowDetail borrowDetail)throws Exception{

		// 创建一个SrtingBuffer,用来拼接sql语句
		StringBuffer sb=new StringBuffer("SELECT bd.*,u.username,b.book_name from borrowdetail bd,user u,book b where u.id=bd.user_id and b.id=bd.book_id");
		//根据查询语句进行sql语句的拼接操作
		if(borrowDetail.getUserId() != null){
			sb.append(" and u.id = ?");
		}
		if(borrowDetail.getStatus() != null){
			sb.append(" and bd.status = ?");
		}
		if(borrowDetail.getBookId() != null){
			sb.append(" and bd.book_id = ?");
		}
		sb.append("  order by bd.id");

		PreparedStatement prepareStatement=(PreparedStatement) con.prepareStatement(sb.toString());
		if(borrowDetail.getUserId() != null){
			prepareStatement.setInt(1, borrowDetail.getUserId());
		}
		if(borrowDetail.getStatus() != null && borrowDetail.getBookId() != null){
			prepareStatement.setInt(2, borrowDetail.getStatus());
			prepareStatement.setInt(3, borrowDetail.getBookId());
		}

		// 执行sql语句
		return prepareStatement.executeQuery();
	}

	// 添加借阅明细信息
	public int add(Connection con, BorrowDetail borrowDetail) throws Exception {
		String sql = "insert into borrowdetail (user_id,book_id,status,borrow_time) values (?,?,?,?)";
		PreparedStatement preparedStatement=(PreparedStatement) con.prepareStatement(sql);
		preparedStatement.setInt(1, borrowDetail.getUserId());
		preparedStatement.setInt(2, borrowDetail.getBookId());
		preparedStatement.setInt(3, borrowDetail.getStatus());
		preparedStatement.setLong(4, borrowDetail.getBorrowTime());
		return preparedStatement.executeUpdate();
	}

	// 还书
	public int returnBook(Connection con,BorrowDetail detail)throws Exception {
		String sql = "update borrowdetail set status = ? ,return_time = ? where id = ?";
		PreparedStatement preparedStatement=(PreparedStatement) con.prepareStatement(sql);
		preparedStatement.setInt(1, detail.getStatus());
		preparedStatement.setLong(2, detail.getReturnTime());
		preparedStatement.setInt(3, detail.getBorrowId());

		return preparedStatement.executeUpdate();
	}
}

```





## 7.  用户登录和注册模块



### 7.1 用户注册



```java
package com.hechaodong.bookmanager.jframe;

import java.awt.*;
import java.sql.*;
import javax.swing.*;

import java.awt.event.FocusEvent;
import java.awt.event.FocusListener;

import com.hechaodong.bookmanager.dao.UserDao;

import com.hechaodong.bookmanager.model.User;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;


// 用户注册界面
// 密码校验的正则表达式： ^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{6,16}$
// 手机号校验的正则表达式：^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))\d{8}$
public class RegFrm extends JFrame {

    private JFrame jf;                          //用户注册的窗体组件
    private JLabel label;                       //展示“用户名”的JLabel
    private JTextField textField;               //输入用户名所对应的文本框
    private JLabel label_1;                     // 展示“密码”的JLabel
    private JTextField textField_1;             //输入密码的文本框
    private JLabel label_2;                     //展示“手机号”的JLabel
    private JTextField textField_2;             //输入手机号所对应的文本框
    private JLabel label_3;                     //展示“性别”的JLabel

    private JRadioButton rdbtnNewRadioButton;   //性别男
    private JRadioButton rdbtnNewRadioButton_1; //性别女

    private JLabel usernameMes;                 //用户名校验结果对应的提示框
    private JLabel passwordMes;                 //密码校验结果对应的提示框
    private JLabel phoneMes;                    //手机号校验结果对应的提示框

    private JLabel label_4;                     //展示“验证码”的JLabel
    private JTextField textField_3;             //输入验证码所对应的文本框
    private ValidCode vcode;                    //展示验证码的图片框
    private JButton button;                     //注册按钮
    private JButton button_1;                   //前往登录按钮

    private JLabel lblNewLabel;                 // 背景图片
    private JLabel lblNewLabel_1;               // 用户注册

    // 创建UserDao对象
    private DbUtil dbUtil = new DbUtil();
    private UserDao userDao = new UserDao();

    public RegFrm() {
        // 初始化窗体
        jf = new JFrame("用户注册");
        jf.getContentPane().setFont(new Font("幼圆", Font.BOLD, 16));
        jf.setBounds(650, 250, 640, 960);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        // 初始化展示“用户名”的JLabel
        label = new JLabel("用户名：");
        label.setForeground(Color.BLACK);
        label.setFont(new Font("幼圆", Font.BOLD, 24));
        label.setBounds(110, 202, 100, 40);
        jf.getContentPane().add(label);

        // 初始化用户名的文本框组件
        textField = new JTextField();
        textField.setFont(new Font("幼圆", Font.BOLD, 14));
        textField.setForeground(Color.BLACK);
        textField.setColumns(10);
        textField.setBounds(202, 202, 164, 30);
        jf.getContentPane().add(textField);

        // 添加焦点事件监听器，当失去焦点的时候需要对用户的用户名进行校验
        textField.addFocusListener(new FocusListener() {
            @Override
            public void focusGained(FocusEvent e) {
            }
            @Override
            public void focusLost(FocusEvent e) {        // 用户名校验
                String text = textField.getText();
                if (ToolUtil.isEmpty(text)) {
                    usernameMes.setText("用户名不能为空");
                    usernameMes.setForeground(Color.RED);
                } else {
                    usernameMes.setText("√");
                    usernameMes.setForeground(Color.GREEN);
                }
            }
        });

        // 初始化展示“密码”的JLabel
        label_1 = new JLabel("密码：");
        label_1.setForeground(Color.BLACK);
        label_1.setFont(new Font("幼圆", Font.BOLD, 24));
        label_1.setBounds(130, 252, 100, 40);
        jf.getContentPane().add(label_1);

        // 初始化密码的文本框组件
        textField_1 = new JTextField();
        textField_1.setFont(new Font("Dialog", Font.BOLD, 14));
        textField_1.setToolTipText("");
        textField_1.setColumns(10);
        textField_1.setBounds(202, 262, 164, 30);
        jf.getContentPane().add(textField_1);

        // 添加焦点事件监听器，当失去焦点的时候需要对用户的密码进行校验
        textField_1.addFocusListener(new FocusListener() {
            @Override
            public void focusLost(FocusEvent e) {
                String pwd = textField_1.getText();
                if (ToolUtil.isEmpty(pwd)) {
                    passwordMes.setText("密码不能为空");
                    passwordMes.setForeground(Color.RED);
                } else {
                    /* 正则表达式
                    * 1. ^(?! [0-9]+$)：以任意字符开头，后面不能全部是数字。
                    * 2. (?![a-zA-Z]+$)：后面不能全部是字母。
                    * 3. [0-9A-Za-z]{6,16}：包含6-16位数字和字母的组合。
                    * 4. $：以任意字符结尾。
                    * */
                    boolean flag = pwd.matches("^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{6,16}$");
                    if (flag) {
                        passwordMes.setText("√");
                        passwordMes.setForeground(Color.GREEN);
                    } else {
                        JOptionPane.showMessageDialog(null, "密码需为6-16位数字和字母的组合");
                        passwordMes.setText("");
                    }
                }
            }

            @Override
            public void focusGained(FocusEvent e) {
            }

        });

        // 初始化展示“手机号”的JLabel
        label_2 = new JLabel("手机号：");
        label_2.setForeground(Color.BLACK);
        label_2.setFont(new Font("幼圆", Font.BOLD, 24));
        label_2.setBounds(110, 302, 100, 60);
        jf.getContentPane().add(label_2);

        // 初始化手机号的文本框组件
        textField_2 = new JTextField();
        textField_2.setFont(new Font("Dialog", Font.BOLD, 14));
        textField_2.setColumns(10);
        textField_2.setBounds(202, 320, 164, 30);
        jf.getContentPane().add(textField_2);

        // 添加焦点事件监听器，当失去焦点的时候需要对用户的手机号进行校验
        textField_2.addFocusListener(new FocusListener() {

            @Override
            public void focusLost(FocusEvent e) {
                String phone = textField_2.getText();
                if (ToolUtil.isEmpty(phone)) {
                    phoneMes.setText("手机号不能为空");
                    phoneMes.setForeground(Color.RED);
                } else {
                    /*
                      1. ^：以任意字符开头。
                      2. ((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))：匹配手机号码的前三位，包括130-139、145、147、150-153、155-159、180、185-189等号段。
                      3. \d{8}：匹配手机号码后8位数字。
                      4. $：以任意字符结尾
                     */
                    boolean flag = phone.matches("^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,5-9]))\\d{8}$");
                    if (flag) {
                        phoneMes.setText("√");
                        phoneMes.setForeground(Color.GREEN);
                    } else {
                        JOptionPane.showMessageDialog(null, "请输入正确的手机号格式");
                        phoneMes.setText("");
                    }
                }
            }

            @Override
            public void focusGained(FocusEvent e) {
            }

        });

        // 初始化展示“性别”的JLabel
        label_3 = new JLabel("性别：");
        label_3.setForeground(Color.BLACK);
        label_3.setFont(new Font("幼圆", Font.BOLD, 24));
        label_3.setBounds(132, 362, 120, 48);
        jf.getContentPane().add(label_3);

		// “男”按钮
        rdbtnNewRadioButton = new JRadioButton("男");
        rdbtnNewRadioButton.setFont(new Font("幼圆", Font.BOLD, 16));
        rdbtnNewRadioButton.setBounds(202, 377, 58, 23);
        jf.getContentPane().add(rdbtnNewRadioButton);

		// “女”按钮
        rdbtnNewRadioButton_1 = new JRadioButton("女");
        rdbtnNewRadioButton_1.setFont(new Font("幼圆", Font.BOLD, 16));
        rdbtnNewRadioButton_1.setBounds(292, 377, 65, 23);
        jf.getContentPane().add(rdbtnNewRadioButton_1);
        ButtonGroup bg = new ButtonGroup();
        bg.add(rdbtnNewRadioButton_1);
        bg.add(rdbtnNewRadioButton);

        // 初始化”用户名“校验结果提示的JLabel
        usernameMes = new JLabel("");
        usernameMes.setFont(new Font("Dialog", Font.BOLD, 15));
        usernameMes.setBounds(372, 202, 122, 27);
        jf.getContentPane().add(usernameMes);

        // 初始化”密码“校验结果提示的JLabel
        passwordMes = new JLabel("");
        passwordMes.setFont(new Font("Dialog", Font.BOLD, 15));
        passwordMes.setBounds(372, 262, 122, 27);
        jf.getContentPane().add(passwordMes);

        // 初始化”手机号“校验结果提示的JLabel
        phoneMes = new JLabel("");
        phoneMes.setFont(new Font("Dialog", Font.BOLD, 15));
        phoneMes.setBounds(372, 324, 122, 30);
        jf.getContentPane().add(phoneMes);

        // 展示验证码的图片框
        vcode = new ValidCode();
        vcode.setLocation(362, 422);
        jf.getContentPane().add(vcode);

        // 初始化展示“验证码”的JLabel
        label_4 = new JLabel("验证码：");
        label_4.setForeground(Color.BLACK);
        label_4.setFont(new Font("幼圆", Font.BOLD, 24));
        label_4.setBounds(110, 420, 100, 40);
        jf.getContentPane().add(label_4);

        // 初始化输入验证码的文本框组件
        textField_3 = new JTextField();
        textField_3.setColumns(18);
        textField_3.setBounds(230, 426, 83, 30);
        jf.getContentPane().add(textField_3);

        // 初始化注册按钮
        button = new JButton("注册");
        // 给注册按钮添加一个动作监听器（校验验证码是否正确）
        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {

                // 获取验证码内容
                String code = textField_3.getText();
                if (ToolUtil.isEmpty(code)) {
                    JOptionPane.showMessageDialog(null, "请输入验证码");
                } else {
                    if (code.equalsIgnoreCase(vcode.getCode())) {
                        RegCheck(e);// 验证码校验成功
                    } else {
                        JOptionPane.showMessageDialog(null, "验证码错误，请重新输入");
                    }
                }
            }
        });
        button.setFont(new Font("幼圆", Font.BOLD, 15));
        button.setBounds(120, 620, 120, 48);
        jf.getContentPane().add(button);

        // 	初始化前往登录界面的按钮
        button_1 = new JButton("前往登录页面");

        // 给登录界面的按钮添加一个动作监听器按钮
        button_1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                jf.setVisible(false);
                new LoginFrm();
            }
        });
        button_1.setFont(new Font("幼圆", Font.BOLD, 15));
        button_1.setBounds(380, 620, 132, 48);
        jf.getContentPane().add(button_1);


        // 初始化”用户注册的“的JLabel
        lblNewLabel_1 = new JLabel("用户注册");
        lblNewLabel_1.setFont(new Font("黑体", Font.BOLD, 33));
        lblNewLabel_1.setForeground(Color.RED); // 设置前景色为红色
        lblNewLabel_1.setBounds(214, 20, 200, 200);
        jf.getContentPane().add(lblNewLabel_1);

        // 初始化界面注册页面背景图片所需的JLabel
        lblNewLabel = new JLabel("");
        lblNewLabel.setForeground(Color.BLACK);
        ImageIcon imageIcon = new ImageIcon("lib/images/1.jpg");
        Image image = imageIcon.getImage();
        image = image.getScaledInstance(640, 960, Image.SCALE_DEFAULT);
        imageIcon.setImage(image);
        lblNewLabel.setIcon(imageIcon);

        lblNewLabel.setBounds(0, 0, 640, 960);
        jf.getContentPane().add(lblNewLabel);

        // 显示页面
        jf.setVisible(true);
        // 是否可以更改jf的大小
        jf.setResizable(false);
    }

    // 完成用户注册
    public void RegCheck(ActionEvent e) {
        // 获取相关组件数据
        String username = textField.getText();
        String password = textField_1.getText();
        String phone = textField_2.getText();
        String sex = "";
        if (rdbtnNewRadioButton.isSelected()) {
            sex = rdbtnNewRadioButton.getText();
        } else {
            sex = rdbtnNewRadioButton_1.getText();
        }
        // 判断数据是否为空
        if (ToolUtil.isEmpty(username) || ToolUtil.isEmpty(password) || ToolUtil.isEmpty(phone)) {
            JOptionPane.showMessageDialog(null, "请输入相关信息");
            return;
        }

        // 把数据封装到User对象中
        User user = new User();
        user.setUserName(username);
        user.setPassword(password);
        user.setSex(sex);
        user.setPhone(phone);
        user.setRole(1);

        // 获取一个连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            int i = userDao.addUser(con, user);// 使用获取的连接和传递进来的"user"对象进行注册。将注册结果存储在名为"i"的整型变量中
            if (i == 2) {
                JOptionPane.showMessageDialog(null, "该用户名已存在,请重新注册");
            } else if (i == 0) {
                JOptionPane.showMessageDialog(null, "注册失败");
            } else {
                JOptionPane.showMessageDialog(null, "注册成功");
                jf.dispose(); // 关闭窗口释放资源
                new LoginFrm();// 打开登录界面
            }
        } catch (Exception e1) {
            e1.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e1) {
                e1.printStackTrace();
            }
        }

    }


    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new RegFrm(); // 注册界面
    }
}

```





### 7.2 验证码



```java
package com.hechaodong.bookmanager.jframe;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.FontMetrics;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.awt.geom.AffineTransform;
import java.util.Random;
 
import javax.swing.JComponent;

// 展示验证码的组件
public class ValidCode extends JComponent implements MouseListener {
 
	private String code;				// 验证码的文本信息
	private int width, height = 40;		// 验证码图片大小
	private int codeLength = 4; 		// 验证码文本信息长度
 
	private Random random = new Random();

	public ValidCode() {
		width = this.codeLength * 16 + (this.codeLength - 1) * 10;
		setPreferredSize(new Dimension(width, height));
		setSize(width, height);
		this.addMouseListener(this);
		setToolTipText("点击可以更换验证码");
	}
 
	public int getCodeLength() {
		return codeLength;
	}
 
	// 设置验证码文字的长度
	public void setCodeLength(int codeLength) {
		if(codeLength < 4) {
			this.codeLength = 4;
		} else {
			this.codeLength = codeLength;
		}
	}
 
	public String getCode() {
		return code;
	}
 
	// 产生随机的颜色
	public Color getRandColor(int min, int max) {
		if (min > 255)
			min = 255;
		if (max > 255)
			max = 255;
		int red = random.nextInt(max - min) + min;
		int green = random.nextInt(max - min) + min;
		int blue = random.nextInt(max - min) + min;
		return new Color(red, green, blue);
	}

	// 设置验证码具体的字母是什么
	public String generateCode() {
		char[] codes = new char[this.codeLength];
		for (int i = 0, len = codes.length; i < len; i++) {
			if (random.nextBoolean()) {
				codes[i] = (char) (random.nextInt(26) + 65);
			} else {
				codes[i] = (char) (random.nextInt(26) + 97);
			}
		}
		this.code = new String(codes);
		return this.code;
	}
 
	@Override
	protected void paintComponent(Graphics g) { // 	Graphics是画笔对象，用来画出验证码
		super.paintComponent(g);
		if(this.code == null || this.code.length() != this.codeLength) {
			this.code = generateCode();
		}

		width = this.codeLength * 16 + (this.codeLength - 1) * 10;
		super.setSize(width, height);
		super.setPreferredSize(new Dimension(width, height));
		Font mFont = new Font("Arial", Font.BOLD | Font.ITALIC, 25);
		g.setFont(mFont);

		//绘制出验证码的背景的矩形轮廓
		Graphics2D g2d = (Graphics2D) g;
		g2d.setColor(getRandColor(200, 250));
		g2d.fillRect(0, 0, width, height);
		g2d.setColor(getRandColor(180, 200));
		g2d.drawRect(0, 0, width - 1, height - 1); // 画一个矩阵

		//绘制出验证码背景的线
		int i = 0, len = 150;
		for (; i < len; i++) {
			int x = random.nextInt(width - 1);
			int y = random.nextInt(height - 1);
			int x1 = random.nextInt(width - 10) + 10;
			int y1 = random.nextInt(height - 4) + 4;
			g2d.setColor(getRandColor(180, 200));
			g2d.drawLine(x, y, x1, y1);  // 画线
		}

		//绘制出验证码的具体字母
		i = 0; len = this.codeLength;
		FontMetrics fm = g2d.getFontMetrics();
		int base = (height - fm.getHeight())/2 + fm.getAscent();
		for(;i<len;i++) {
			int b = random.nextBoolean() ? 1 : -1;
			g2d.rotate(random.nextInt(10)*0.01*b);
			g2d.setColor(getRandColor(20, 130));
			g2d.drawString(code.charAt(i)+"", 16 * i + 10, base);// 从二维字符中获取对应的字符将其划到界面中
		}
	}
 
	//下一个验证码
	public void nextCode() {
		generateCode();	// 重新生成一个4位数的验证码
		repaint();		// 重新渲染组件
	}
 
	@Override
	public void mouseClicked(MouseEvent e) {
		nextCode();
	}
 
	@Override
	public void mousePressed(MouseEvent e) {
		
	}
 
	@Override
	public void mouseReleased(MouseEvent e) {
		
	}
 
	@Override
	public void mouseEntered(MouseEvent e) {
		
	}
 
	@Override
	public void mouseExited(MouseEvent e) {
		
	}
}
```





### 7.3 用户登录

```java
package com.hechaodong.bookmanager.jframe;

import java.awt.*;
import java.sql.*;
import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPasswordField;

import com.hechaodong.bookmanager.dao.UserDao;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;
import com.hechaodong.bookmanager.model.User;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;

import javax.swing.JTextField;
import javax.swing.JComboBox;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

// 用户登录界面
public class LoginFrm extends JFrame {

    public static User currentUser;             // 当登录成功后，使用该变量存储登录的用户
    private JFrame jf;                          // 登录界面的窗体结构
    private JTextField userNameText;            // 输入用户名的文本框
    private JTextField passwordText;            // 输入密码的文本框
    private JComboBox<String> comboBox;         // 用户选项的下拉选择框

    private UserDao userDao = new UserDao();
    private DbUtil dbUtil = new DbUtil();

    public LoginFrm() {
        // 初始化窗体组件
        jf = new JFrame("图书管理");
        jf.getContentPane().setFont(new Font("幼圆", Font.BOLD, 14));
        jf.setBounds(650, 250, 640, 960);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        // 初始化登录界面的图片
        JLabel lblNewLabel = new JLabel();
        ImageIcon imageIcon = new ImageIcon("lib/images/2.jpg");
        Image image = imageIcon.getImage();
        image = image.getScaledInstance(280, 168, Image.SCALE_DEFAULT);
        imageIcon.setImage(image);
        lblNewLabel.setIcon(imageIcon);

        lblNewLabel.setBounds(180, 72, 430, 218);
        jf.getContentPane().add(lblNewLabel);

        // 初始化展示“用户名”的JLabel
        JLabel label = new JLabel("用户名：");
        label.setFont(new Font("黑体", Font.BOLD, 24));
        label.setBounds(150, 292, 100, 100);
        jf.getContentPane().add(label);

        // 初始化用户名的文本框组件
        userNameText = new JTextField();
        userNameText.setBounds(250, 322, 142, 40);
        jf.getContentPane().add(userNameText);
        userNameText.setColumns(10);

        // 初始化展示“密码”的JLabel
        JLabel label_1 = new JLabel("密码：");
        label_1.setFont(new Font("黑体", Font.BOLD, 24));
        label_1.setBounds(170, 362, 100, 100);
        jf.getContentPane().add(label_1);

        // 初始化密码的文本框组件
        passwordText = new JPasswordField();
        passwordText.setColumns(10);
        passwordText.setBounds(250, 392, 142, 40);
        jf.getContentPane().add(passwordText);

        // 初始化展示“权限”的JLabel
        JLabel label_2 = new JLabel("权限：");
        label_2.setFont(new Font("黑体", Font.BOLD, 24));
        label_2.setBounds(172, 442, 80, 80);
        jf.getContentPane().add(label_2);

        // 初始权限的文本框组件
        comboBox = new JComboBox();
        comboBox.setBounds(250, 462, 142, 40);
        comboBox.addItem("用户");
        comboBox.addItem("管理员");
        jf.getContentPane().add(comboBox); // 用户-----管理员

        // 登录按钮
        JButton button = new JButton("登录");
        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                checkLogin(e); // 检查登录（获取数据比对数据库信息）
            }
        });
        button.setBounds(150, 650, 120, 48);
        jf.getContentPane().add(button);

        // 注册按钮
        JButton button_1 = new JButton("注册");
        button_1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                regUser(e); // 跳转到注册界面
            }
        });
        button_1.setBounds(350, 650, 120, 48);
        jf.getContentPane().add(button_1);

        // 登录界面背景图
        JLabel lblNewLabel_1 = new JLabel("");
        lblNewLabel_1.setIcon(new ImageIcon("lib/images/3.jpg"));
        lblNewLabel_1.setBounds(0, 0, 640, 940);
        jf.getContentPane().add(lblNewLabel_1);


        // 显示界面，不可以调整界面大小
        jf.setVisible(true);
        jf.setResizable(false);

    }

    // 跳转到注册页面
    public void regUser(ActionEvent e) {
        jf.setVisible(false);
        new RegFrm();

    }

    // 用户登录的逻辑操作（获取数据并校对数据库数据是否一致）
    public void checkLogin(ActionEvent e) {
        // 获取用户登录信息
        String userName = userNameText.getText();
        String password = passwordText.getText();
        int index = comboBox.getSelectedIndex(); // 权限
        if (ToolUtil.isEmpty(userName) || ToolUtil.isEmpty(password)) {
            JOptionPane.showMessageDialog(null, "用户名和密码不能为空");
            return;
        }

        // 把数据封装到User对象中
        User user = new User();
        user.setUserName(userName);
        user.setPassword(password);
        if (index == 0) {
            user.setRole(1);// 用户
        } else {
            user.setRole(2);// 管理员
        }

        // 获取一个连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection(); // 获取数据库连接
            User login = userDao.login(con, user);// 使用获取的连接和传递进来的"user"对象进行登录验证
            currentUser = login;
            if (login == null) {
                JOptionPane.showMessageDialog(null, "登录失败");
            } else {
                // 权限 1普通 2管理员
                if (index == 0) {
                    jf.dispose(); // 释放与当前窗口关联的所有资源
                    new UserMenuFrm(); // 用户界面
                } else {
                    jf.dispose();// 释放与当前窗口关联的所有资源
                    new AdminMenuFrm(); // 管理员界面
                }
            }
        } catch (Exception e21) {
            e21.printStackTrace();
            JOptionPane.showMessageDialog(null, "登录异常");
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e31) {
                e31.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new LoginFrm();
    }
}

```









## 8. 图书借还模块



### 8.1 用户操作界面

```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.Color;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.sql.ResultSet;
import java.util.Vector;

import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.UIManager;
import javax.swing.border.TitledBorder;
import javax.swing.table.DefaultTableModel;

import com.hechaodong.bookmanager.dao.BorrowDetailDao;
import com.hechaodong.bookmanager.dao.BookDao;
import com.hechaodong.bookmanager.model.BorrowDetail;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import com.hechaodong.bookmanager.model.Book;

import javax.swing.ImageIcon;


public class UserMenuFrm extends JFrame {
    private JFrame jf;                  // 主界面的JFrame窗口
    private JLabel lblNewLabel_1;       // 展示当前登录用户的用户名所需要的JLabel
    private JLabel lblNewLabel_2;       // 展示顶部“欢迎你”的JLabel
    private JTable table;               // 借阅信息的表格组件
    private DefaultTableModel model;    // 借阅信息的表格组件所需要的数据模型对象
    private JTextField textField;       // 输入换书编号的文本框textField
    private JButton btnBackBook;        // 换书按钮
    private JButton button;             // 退出系统按钮
    private JPanel panel_2;             // 初始化展示图书信息所需要的面板
    private JComboBox comboBox;         // 搜索字段所需要的下拉选择框
    private JTextField textField_1;     // 搜索关键字所需要的文本框
    private JButton button_1;           // 查询按钮
    private JTable BookTable;           // 展示图书信息所需要的表格组件
    private DefaultTableModel BookModel;// 展示图书信息所需要的表格组件的数据模型组件
    private JTextField textField_2;     // 展示借书编号所需要的文本框组件
    private JTextField textField_3;     // 展示借书书名所需要的文本框组件
    private JLabel lblNewLabel_3;       // 展示背景图片所需要的JLabel

    private DbUtil dbUtil = new DbUtil();
    private BorrowDetailDao borrowDetailDao = new BorrowDetailDao();
    private BookDao BookDao = new BookDao();

    public UserMenuFrm() {

        // 初始化用户操作界面
        jf = new JFrame();
        jf.setTitle("用户页面");
        jf.setBounds(650, 250, 691, 896);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        // 顶部展示”借阅信息“的JPanel
        JPanel panel_1 = new JPanel();
        panel_1.setBorder(new TitledBorder(UIManager.getBorder("TitledBorder.border"), "借阅信息", TitledBorder.LEADING, TitledBorder.TOP, null, new Color(255, 0, 0)));
        panel_1.setBounds(23, 48, 651, 239);

        // 表头栏数据
        String[] title = {"编号", "书名", "状态", "借书时间", "还书时间"};// 一维数组
        // 具体的各栏行记录 先用空的二位数组占位
        String[][] dates = {};


        // 初始化表格组件以及数据模型组件 （然后实例化 上面2个控件对象）
        model = new DefaultTableModel(dates, title);
        table = new JTable();
        table.setModel(model);

        // 获取数据库数据放置table中
        putDates(new BorrowDetail());

        // 将表格组件添加到JScrollPane中，并将JScrollPane添加到panel_1中，最后将panel_1添加到JFrame中
        panel_1.setLayout(null);
        JScrollPane jscrollpane = new JScrollPane();
        jscrollpane.setBounds(20, 22, 607, 188);
        jscrollpane.setViewportView(table);
        panel_1.add(jscrollpane);
        jf.getContentPane().add(panel_1);

        // 顶部问候语
        lblNewLabel_1 = new JLabel("New label");
        lblNewLabel_1.setForeground(Color.RED);
        lblNewLabel_1.setFont(new Font("Dialog", Font.BOLD, 18));
        lblNewLabel_1.setBounds(315, 0, 197, 28);
        jf.getContentPane().add(lblNewLabel_1);
        lblNewLabel_1.setText(LoginFrm.currentUser.getUserName());

        lblNewLabel_2 = new JLabel("欢迎来到知识的海洋 ");
        lblNewLabel_2.setFont(new Font("Dialog", Font.BOLD, 18));
        lblNewLabel_2.setBounds(254, 4, 258, 68);
        jf.getContentPane().add(lblNewLabel_2);

        // 还书操作界面的JPanel
        JPanel panel = new JPanel();
        panel.setBorder(new TitledBorder(UIManager.getBorder("TitledBorder.border"), "还书", TitledBorder.LEADING, TitledBorder.TOP, null, new Color(255, 0, 0)));
        panel.setBounds(23, 294, 651, 70);
        jf.getContentPane().add(panel);
        panel.setLayout(null);


        // 展示“编号”的JLabel
        JLabel lblNewLabel = new JLabel("编号：");
        lblNewLabel.setBounds(90, 25, 51, 27);
        panel.add(lblNewLabel);
        lblNewLabel.setFont(new Font("幼圆", Font.BOLD, 16));

        // 初始化编号所对应的文本框组件
        textField = new JTextField();
        textField.setBounds(145, 28, 116, 24);
        panel.add(textField);
        textField.setColumns(10);

        // 初始化还书按钮
        btnBackBook = new JButton("还书");
        btnBackBook.setFont(new Font("Dialog", Font.BOLD, 15));
        btnBackBook.setBounds(299, 25, 85, 31);
        panel.add(btnBackBook);

        // 初始化退出系统按钮
        button = new JButton("退出系统");
        button.setFont(new Font("Dialog", Font.BOLD, 15));
        button.setBounds(407, 25, 103, 31);
        panel.add(button);

        // 初始化展示展示图书信息的面板
        panel_2 = new JPanel();
        panel_2.setBorder(new TitledBorder(null, "借阅信息", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel_2.setBounds(23, 374, 651, 346);
        jf.getContentPane().add(panel_2);
        panel_2.setLayout(null);

        // 初始化查询关所对应的文本框组件
        textField_1 = new JTextField();
        textField_1.setColumns(10);
        textField_1.setBounds(252, 23, 135, 27);
        panel_2.add(textField_1);

        // 初始化查询按钮组件
        button_1 = new JButton("查询");
        button_1.addActionListener(new ActionListener() {       // 业务查询的代码逻辑

            public void actionPerformed(ActionEvent e) {

                // 获取查询字段
                int index = comboBox.getSelectedIndex();
                if (index == 0) { // 书名查询
                    String bookName = textField_1.getText();
                    Book book = new Book();
                    book.setBookName(bookName);
                    putDates(book);
                } else {          // 作者名查询
                    String authoerName = textField_1.getText();
                    Book book = new Book();
                    book.setAuthor(authoerName);
                    putDates(book);
                }
            }
        });
        // 查询按钮
        button_1.setFont(new Font("幼圆", Font.BOLD, 16));
        button_1.setBounds(408, 20, 93, 33);
        panel_2.add(button_1);


        // 初始化查询字段所对应的下拉选择框组件
        comboBox = new JComboBox();
        comboBox.setFont(new Font("幼圆", Font.BOLD, 15));
        comboBox.setBounds(123, 26, 109, 24);
        comboBox.addItem("书籍名称");
        comboBox.addItem("书籍作者");
        panel_2.add(comboBox);

        // 展示图书信息所对应的表头数据
        String[] BookTitle = {"编号", "书名", "类型", "作者", "描述"};

        // 具体的各栏行记录 先用空的二位数组占位
        String[][] BookDates = {};

        // 建立数据模型，实例化上面2个控件对象
        BookModel = new DefaultTableModel(BookDates, BookTitle);
        BookTable = new JTable(BookModel);

        // 获取数据库数据放置table中
        putDates(new Book());

        // 将bookTable添加到JScrollPane中，再将JScrollPane添加到panel_2中，最后将panel_2添加到JFrame中
        panel_2.setLayout(null);
        JScrollPane jscrollpane1 = new JScrollPane();
        jscrollpane1.setBounds(22, 74, 607, 250);
        jscrollpane1.setViewportView(BookTable);
        panel_2.add(jscrollpane1);
        jf.getContentPane().add(panel_2);

        // 创建展示借书的面板
        JPanel panel_3 = new JPanel();
        panel_3.setBorder(new TitledBorder(null, "借书", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel_3.setBounds(23, 730, 645, 87);
        jf.getContentPane().add(panel_3);
        panel_3.setLayout(null);

        // 初始化展示编号两个字所需要的JLabel
        JLabel label = new JLabel("编号：");
        label.setFont(new Font("Dialog", Font.BOLD, 15));
        label.setBounds(68, 31, 48, 33);
        panel_3.add(label);

        // 初始化展示所借图书编号所需要的文本框组件
        textField_2 = new JTextField();
        textField_2.setEditable(false);
        textField_2.setColumns(10);
        textField_2.setBounds(126, 34, 135, 27);
        panel_3.add(textField_2);

        // 初始化展示书名两个字所需要的JLabel
        JLabel label_1 = new JLabel("书名：");
        label_1.setFont(new Font("Dialog", Font.BOLD, 15));
        label_1.setBounds(281, 31, 48, 33);
        panel_3.add(label_1);

        // 初始化展示所借书名所需要的文本框组件
        textField_3 = new JTextField();
        textField_3.setEditable(false);
        textField_3.setColumns(10);
        textField_3.setBounds(339, 34, 135, 27);
        panel_3.add(textField_3);


        // 创建借书按钮
        JButton button_2 = new JButton("借书");
        button_2.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {

                // 获取要借的书所对应的编号及其书名
                String bookId = textField_2.getText();
                String bookName = textField_3.getText();
                if (ToolUtil.isEmpty(bookId) || ToolUtil.isEmpty(bookName)) {
                    JOptionPane.showMessageDialog(null, "请选择相关书籍");
                    return;
                }
                // 把要借的书的相关信息封装成一个BorrowDetail
                BorrowDetail borrowDetail = new BorrowDetail();
                borrowDetail.setUserId(LoginFrm.currentUser.getUserId());
                borrowDetail.setBookId(Integer.parseInt(bookId));
                borrowDetail.setStatus(1);
                borrowDetail.setBorrowTime(ToolUtil.getTime());

                // 获取连接对象
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    ResultSet list = borrowDetailDao.list(con, borrowDetail);//先查询是否有该书
                    while (list.next()) {
                        JOptionPane.showMessageDialog(null, "该书已在借,请先还再借");
                        return;
                    }
                    // 保存借阅信息
                    int i = borrowDetailDao.add(con, borrowDetail);
                    // 对返回结果进行判断
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "借书成功");
                        putDates(new BorrowDetail());
                    } else {
                        JOptionPane.showMessageDialog(null, "借书失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "借书异常");
                } finally {
                    try {
                        dbUtil.closeCon(con);
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }
            }
        });
        button_2.setFont(new Font("Dialog", Font.BOLD, 16));
        button_2.setBounds(495, 31, 80, 33);
        panel_3.add(button_2);

        // 初始化展示背景图片所需要的JLabel
        lblNewLabel_3 = new JLabel("");
        lblNewLabel_3.setIcon(new ImageIcon("lib/images/7.png"));
        lblNewLabel_3.setBounds(0, 0, 684, 864);
        jf.getContentPane().add(lblNewLabel_3);

        // 给借书的表格添加一个鼠标监听器
        BookTable.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                tableMousePressed(evt);
            }
        });

        // 给退出系统添加一个动作监听按钮
        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                JOptionPane.showMessageDialog(null, "欢迎再次使用");
                jf.dispose();
            }
        });
        btnBackBook.setVisible(false);// 关闭窗口

        // 给还书按钮添加一个动作监听按钮
        btnBackBook.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {

                // 获取还书信息的编号
                String BorrowStr = textField.getText();
                if (ToolUtil.isEmpty(BorrowStr)) {
                    JOptionPane.showMessageDialog(null, "请选择未还的书籍");
                    return;
                }

                // 创建BorrowDetail对象，封装还书所对应的数据
                BorrowDetail detail = new BorrowDetail();
                detail.setBorrowId(Integer.parseInt(BorrowStr));
                detail.setStatus(2);
                detail.setReturnTime(ToolUtil.getTime());

                // 获取连接对象
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    int i = borrowDetailDao.returnBook(con, detail);
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "还书成功");
                    } else {
                        JOptionPane.showMessageDialog(null, "还书失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "还书异常");
                } finally {
                    try {
                        dbUtil.closeCon(con);
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }

                // 重新查询借阅信息
                putDates(new BorrowDetail());
            }
        });

        // 让jf可以显示，并且可以更改jf的大小
        jf.setVisible(true);
        jf.setResizable(true);
    }

    public void tableMousePressed(MouseEvent evt) {

        // 获取当前用户所选择的数据行，然后将该行的数据在借书面板的相关组件中进行展示
        int row = BookTable.getSelectedRow();
        Object bookId = BookTable.getValueAt(row, 0);
        Object bookName = BookTable.getValueAt(row, 1);
        textField_2.setText(bookId.toString());
        textField_3.setText(bookName.toString());
    }

    //从数据库获取书籍信息
    public void putDates(Book book) {
        DefaultTableModel model = (DefaultTableModel) BookTable.getModel();
        model.setRowCount(0);// 将表格的行数设置为0，即清空表格中的所有行数据

        // 获取连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            book.setStatus(1);// 给book对象设置sataus属性为1 上架
            ResultSet list = BookDao.list(con, book);// 调用BookDao中的方法进行查询
            while (list.next()) {
                Vector rowData = new Vector();
                rowData.add(list.getInt("id"));
                rowData.add(list.getString("book_name"));
                rowData.add(list.getString("type_name"));
                rowData.add(list.getString("author"));
                rowData.add(list.getString("remark"));
                model.addRow(rowData);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    public void putDates(BorrowDetail borrowDetail) {
        DefaultTableModel model = (DefaultTableModel) table.getModel();
        model.setRowCount(0);
        Integer userId = LoginFrm.currentUser.getUserId();
        Connection con = null;

        // 获取连接对象
        try {
            con = dbUtil.getConnection();
            borrowDetail.setUserId(userId);
            ResultSet list = borrowDetailDao.list(con, borrowDetail);
            while (list.next()) {
                Vector rowData = new Vector();
                rowData.add(list.getInt("id"));
                rowData.add(list.getString("book_name"));
                int status = list.getInt("status");
                if (status == 1) {
                    rowData.add("在借");
                }
                if (status == 2) {
                    rowData.add("已还");
                }
                rowData.add(ToolUtil.getDateByTime(list.getLong("borrow_time")));
                if (status == 2) {
                    rowData.add(ToolUtil.getDateByTime(list.getLong("return_time")));
                }
                model.addRow(rowData);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

        // 添加一个鼠标监听器
        table.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent me) {
                putBack(me);
            }
        });
    }

    protected void putBack(MouseEvent me) {

        // 获取用户所选的行信息
        int row = table.getSelectedRow();
        Integer borrowId = (Integer) table.getValueAt(row, 0);
        String status = (String) table.getValueAt(row, 2);
        textField.setText(borrowId.toString());
        if (status.equals("在借")) {
            this.btnBackBook.setVisible(true);
        } else {
            this.btnBackBook.setVisible(false);
        }

    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new UserMenuFrm();
    }
}
```





## 9. 书籍管理模块



### 9.1 管理员操作界面



```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

import javax.swing.JFrame;

import com.hechaodong.bookmanager.dao.BookTypeDao;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import com.hechaodong.bookmanager.model.BookType;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;

import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JLabel;
import javax.swing.JTextField;

import java.awt.Font;

import javax.swing.JButton;

import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

import javax.swing.JTextArea;

import java.awt.Color;
import javax.swing.ImageIcon;

public class AdminMenuFrm extends JFrame {

	private JFrame jf;					// 主操作界面所对应的窗体
	private JTextField textField;		// 输入类别名称所需要的文本框组件
	private JButton btnNewButton;		//添加按钮
	private JTextArea textArea;			//输入类别详情信息所需要的文本框组件

	private DbUtil dbUtil=new DbUtil();
	private BookTypeDao bookTypeDao=new BookTypeDao();


	public AdminMenuFrm(){

		// 初始化主界面所对应的窗体组件
		jf=new JFrame("管理员界面");
		jf.setBounds(650, 250, 600, 429);
		jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		jf.getContentPane().setLayout(null);

		// 初始化展示“类别名称”的 JLabel
		JLabel label = new JLabel();
		label.setFont(new Font("幼圆", Font.BOLD, 14));
		label.setText("类别说明：");
		label.setBounds(112, 107, 75, 26);
		jf.getContentPane().add(label);

		// 初始化展示“类别说明”的JLabel
		JLabel label_1 = new JLabel();
		label_1.setFont(new Font("幼圆", Font.BOLD, 14));
		label_1.setText("类别名称：");
		label_1.setBounds(112, 38, 75, 26);
		jf.getContentPane().add(label_1);

		// 初始化输入类别名称所需要的文本框组件
		textField = new JTextField();
		textField.setBounds(197, 38, 241, 26);
		jf.getContentPane().add(textField);

		// 初始化添加按钮
		btnNewButton = new JButton("添加");
		btnNewButton.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {

				// 获取类别名称和类别说明数据
				String typeName = textField.getText();
				String typeRemark = textArea.getText();
				// 判断数据
				if (ToolUtil.isEmpty(typeName) || ToolUtil.isEmpty(typeRemark)) {
					JOptionPane.showMessageDialog(null, "请输入相关信息");
					return;
				}

				// 把数据封装到BookType对象
				BookType bookType = new BookType();
				bookType.setTypeName(typeName);
				bookType.setRemark(typeRemark);

				// 获取连接对象
				Connection con = null;
				try {
					// 把数据保存到数据库中
					con = dbUtil.getConnection();
					int i = bookTypeDao.add(con, bookType);
					if (i == 1) {
						JOptionPane.showMessageDialog(null, "添加成功");
						reset();
					}else if(i == 2){
						JOptionPane.showMessageDialog(null, "添加失败,类别已存在");
					} else {
						JOptionPane.showMessageDialog(null, "添加失败");
					}
				} catch (Exception e1) {
					e1.printStackTrace();
				}finally{
					try {
						dbUtil.closeCon(con);
					} catch (Exception e1) {
						e1.printStackTrace();
					}
				}
			}
		});
		btnNewButton.setFont(new Font("幼圆", Font.BOLD, 14));
		btnNewButton.setBounds(182, 281, 80, 26);
		jf.getContentPane().add(btnNewButton);

		// 初始化重置按钮
		JButton button = new JButton("重置");
		button.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				reset(); // 清空数据
			}
		});
		button.setFont(new Font("幼圆", Font.BOLD, 14));
		button.setBounds(360, 281, 80, 26);
		jf.getContentPane().add(button);

		// 初始化类别详细信息所需要的文本域组件
		textArea = new JTextArea();
		textArea.setColumns(20);
		textArea.setRows(5);
		textArea.setBackground(Color.WHITE);
		textArea.setBounds(197, 109, 241, 132);
		jf.getContentPane().add(textArea);


		// 初始化展示背景图片所需要的JLabel
		JLabel lblNewLabel = new JLabel("");
		lblNewLabel.setIcon(new ImageIcon("lib/images/6.png"));
		lblNewLabel.setBounds(0, 0, 584, 370);
		jf.getContentPane().add(lblNewLabel);

		// 创建菜单栏组件
		JMenuBar menuBar = new JMenuBar();
		jf.setJMenuBar(menuBar);

		// 添加类别管理
		JMenu mnNewMenu = new JMenu("类别管理");
		menuBar.add(mnNewMenu);

		// 添加类别添加菜单项
		JMenuItem mntmNewMenuItem = new JMenuItem("类别添加");
		mnNewMenu.add(mntmNewMenuItem);

		// 添加类别修改菜单项
		JMenuItem mntmNewMenuItem_1 = new JMenuItem("类别修改");
		mntmNewMenuItem_1.addMouseListener(new MouseAdapter() {
			public void mousePressed(MouseEvent evt) {
				jf.dispose();
				new AdminBTypeEdit();
			}
		});
		mnNewMenu.add(mntmNewMenuItem_1);

		// 添加书籍管理菜单
		JMenu mnNewMenu_2 = new JMenu("书籍管理");
		menuBar.add(mnNewMenu_2);

		// 添加书籍添加菜单
		JMenuItem mntmNewMenuItem_2 = new JMenuItem("书籍添加");
		mntmNewMenuItem_2.addMouseListener(new MouseAdapter() {
			public void mousePressed(MouseEvent evt) {
				jf.dispose();
				new AdminBookAdd();
			}
		});
		mnNewMenu_2.add(mntmNewMenuItem_2);

		//添加书籍修改菜单
		JMenuItem mntmNewMenuItem_3 = new JMenuItem("书籍修改");
		mntmNewMenuItem_3.addMouseListener(new MouseAdapter() {
			public void mousePressed(MouseEvent evt) {
				jf.dispose();
				new AdminBookEdit();
			}
		});
		mnNewMenu_2.add(mntmNewMenuItem_3);

		// 添加用户管理菜单
		JMenu menu1 = new JMenu("用户管理");
		menuBar.add(menu1);

		// 添加用户信息菜单
		JMenuItem mntmNewMenuItem_4 = new JMenuItem("用户信息");
		mntmNewMenuItem_4.addMouseListener(new MouseAdapter() {
			public void mousePressed(MouseEvent evt) {
				jf.dispose();
				new AdminUserInfo();
			}
		});
		menu1.add(mntmNewMenuItem_4);

		// 添加借阅信息菜单
		JMenuItem mntmNewMenuItem_5 = new JMenuItem("借阅信息");
		mntmNewMenuItem_5.addMouseListener(new MouseAdapter() {
			public void mousePressed(MouseEvent evt) {
				jf.dispose();
				new AdminBorrowInfo();
			}
		});
		menu1.add(mntmNewMenuItem_5);

		// 添加退出系统菜单
		JMenu mnNewMenu_1 = new JMenu("退出系统");
		mnNewMenu_1.addMouseListener(new MouseAdapter() {
			public void mousePressed(MouseEvent evt) {
				JOptionPane.showMessageDialog(null, "欢迎再次使用");
				jf.dispose();
			}
		});
		menuBar.add(mnNewMenu_1);

		// 让jf显示，并且可以更改jf大小
		jf.setVisible(true);
		jf.setResizable(true);
	}
	// 清空类别数据
	public void reset() {
		textField.setText("");
		textArea.setText("");
	}

	public static void main(String[] args) {
		try {
			BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
			BeautyEyeLNFHelper.launchBeautyEyeLNF();
		} catch (Exception e) {
			e.printStackTrace();
		}
		new AdminMenuFrm();
	}
}

```





### 9.2 图书的添加



```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

import javax.swing.JFrame;

import com.hechaodong.bookmanager.dao.BookTypeDao;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import com.hechaodong.bookmanager.dao.BookDao;
import com.hechaodong.bookmanager.model.Book;
import com.hechaodong.bookmanager.model.BookType;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;

import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.border.TitledBorder;

import java.awt.Color;

import javax.swing.JLabel;

import java.awt.Font;

import javax.swing.JTextField;
import javax.swing.JButton;

import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.math.BigDecimal;
import java.sql.ResultSet;

import javax.swing.JComboBox;
import javax.swing.ImageIcon;


public class AdminBookAdd extends JFrame {

    private JFrame jf;
    private JTextField textField;
    private JTextField textField_1;
    private JTextField textField_2;
    private JTextField textField_3;
    private JTextField textField_4;
    private JTextField textField_6;
    private JComboBox comboBox;
    BookDao bookDao = new BookDao();
    DbUtil dbUtil = new DbUtil();
    BookTypeDao bookTypeDao = new BookTypeDao();

    public AdminBookAdd() {
        // 初始化书籍添加界面
        jf = new JFrame("书籍添加");
        jf.setBounds(650, 250, 600, 378);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        // 顶部展示“书籍添加”的JLabel
        JPanel panel = new JPanel();
        panel.setBorder(new TitledBorder(null, "书籍添加", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel.setBounds(23, 21, 540, 275);
        jf.getContentPane().add(panel);
        panel.setLayout(null);

        // 初始化展示“书名”的JLabel
        JLabel lblNewLabel = new JLabel("书名：");
        lblNewLabel.setFont(new Font("幼圆", Font.BOLD, 14));
        lblNewLabel.setBounds(58, 31, 45, 27);
        panel.add(lblNewLabel);

        // 初始化输入书名的文本框组件
        textField = new JTextField();
        textField.setBounds(101, 31, 129, 27);
        panel.add(textField);
        textField.setColumns(10);

        // 初始化展示“作者”的JLabel
        JLabel label = new JLabel("作者：");
        label.setFont(new Font("幼圆", Font.BOLD, 14));
        label.setBounds(294, 31, 45, 27);
        panel.add(label);

        // 初始化输入作者的文本框组件
        textField_1 = new JTextField();
        textField_1.setColumns(10);
        textField_1.setBounds(338, 31, 128, 27);
        panel.add(textField_1);

        // 初始化展示“出版社”的JLabel
        JLabel label_1 = new JLabel("出版社：");
        label_1.setFont(new Font("幼圆", Font.BOLD, 14));
        label_1.setBounds(43, 79, 60, 27);
        panel.add(label_1);

        // 初始化输入出版社的文本框组件
        textField_2 = new JTextField();
        textField_2.setColumns(10);
        textField_2.setBounds(101, 79, 129, 27);
        panel.add(textField_2);


        // 初始化展示“库存”的JLabel
        JLabel label_2 = new JLabel("库存：");
        label_2.setFont(new Font("幼圆", Font.BOLD, 14));
        label_2.setBounds(58, 125, 45, 27);
        panel.add(label_2);

        // 初始化输入库存的文本框组件
        textField_3 = new JTextField();
        textField_3.setColumns(10);
        textField_3.setBounds(101, 125, 129, 27);
        panel.add(textField_3);

        // 初始化展示“价格”的JLabel
        JLabel label_3 = new JLabel("价格：");
        label_3.setFont(new Font("幼圆", Font.BOLD, 14));
        label_3.setBounds(294, 79, 45, 27);
        panel.add(label_3);

        // 初始化输入价格的文本框组件
        textField_4 = new JTextField();
        textField_4.setColumns(10);
        textField_4.setBounds(337, 79, 129, 27);
        panel.add(textField_4);

        // 初始化展示“类别”的JLabel
        JLabel label_4 = new JLabel("类别：");
        label_4.setFont(new Font("幼圆", Font.BOLD, 14));
        label_4.setBounds(294, 125, 45, 27);
        panel.add(label_4);

        // 初始化展示“描述”的JLabel
        JLabel label_5 = new JLabel("描述：");
        label_5.setFont(new Font("幼圆", Font.BOLD, 14));
        label_5.setBounds(58, 170, 45, 27);
        panel.add(label_5);

        // 初始化输入描述的文本框组件
        textField_6 = new JTextField();
        textField_6.setColumns(10);
        textField_6.setBounds(101, 173, 365, 27);
        panel.add(textField_6);

        // 添加按钮
        JButton btnNewButton = new JButton("添加");
        // 给添加按钮添加一个动作监听器
        btnNewButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String bookName = textField.getText();
                String author = textField_1.getText();
                String publish = textField_2.getText();
                String priceStr = textField_4.getText();
                String numberStr = textField_3.getText();
                String remark = textField_6.getText();
                if (ToolUtil.isEmpty(bookName) || ToolUtil.isEmpty(author)
                        || ToolUtil.isEmpty(publish) || ToolUtil.isEmpty(priceStr)
                        || ToolUtil.isEmpty(numberStr) || ToolUtil.isEmpty(remark)) {
                    JOptionPane.showMessageDialog(null, "请输入相关内容");
                    return;
                }
                BookType selectedItem = (BookType) comboBox.getSelectedItem();
                Integer typeId = selectedItem.getTypeId();
                int number;
                double price;
                try {
                    number = Integer.parseInt(numberStr);
                    price = new BigDecimal(priceStr).setScale(2, BigDecimal.ROUND_DOWN)
                            .doubleValue();
                } catch (Exception e1) {
                    JOptionPane.showMessageDialog(null, "参数错误");
                    return;
                }

                // 封装数据
                Book book = new Book();
                book.setBookName(bookName);
                book.setAuthor(author);
                book.setBookTypeId(typeId);
                book.setNumber(number);
                book.setPrice(price);
                book.setPublish(publish);
                book.setRemark(remark);
                book.setStatus(1);
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    int i = bookDao.add(con, book);
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "添加成功");
                        reset();
                    } else {
                        JOptionPane.showMessageDialog(null, "添加失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "添加异常");
                }
            }
        });
        btnNewButton.setFont(new Font("幼圆", Font.BOLD, 14));
        btnNewButton.setBounds(124, 227, 77, 27);
        panel.add(btnNewButton);

        // 重置按钮
        JButton button = new JButton("重置");
        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                reset();
            }
        });
        button.setFont(new Font("幼圆", Font.BOLD, 14));
        button.setBounds(329, 229, 77, 27);
        panel.add(button);

        // 类别 文本下拉框
        comboBox = new JComboBox();
        comboBox.setBounds(338, 126, 128, 26);
        panel.add(comboBox);

        // 背景图片
        JLabel lblNewLabel_1 = new JLabel("");
        lblNewLabel_1.setIcon(new ImageIcon("lib/images/4.png"));
        lblNewLabel_1.setBounds(0, -4, 584, 323);
        jf.getContentPane().add(lblNewLabel_1);
        getBookType();

        // 初始化菜单栏
        JMenuBar menuBar = new JMenuBar();
        jf.setJMenuBar(menuBar);

        JMenu mnNewMenu = new JMenu("类别管理");
        menuBar.add(mnNewMenu);

        JMenuItem mntmNewMenuItem = new JMenuItem("类别添加");
        mntmNewMenuItem.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminMenuFrm();
            }
        });
        mnNewMenu.add(mntmNewMenuItem);

        JMenuItem mntmNewMenuItem_1 = new JMenuItem("类别修改");
        mntmNewMenuItem_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBTypeEdit();
            }
        });
        mnNewMenu.add(mntmNewMenuItem_1);

        JMenu mnNewMenu_2 = new JMenu("书籍管理");
        menuBar.add(mnNewMenu_2);

        JMenuItem mntmNewMenuItem_2 = new JMenuItem("书籍添加");
        mnNewMenu_2.add(mntmNewMenuItem_2);

        JMenuItem mntmNewMenuItem_3 = new JMenuItem("书籍修改");
        mntmNewMenuItem_3.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookEdit();
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_3);

        JMenu menu1 = new JMenu("用户管理");
        menuBar.add(menu1);

        JMenuItem mntmNewMenuItem_4 = new JMenuItem("用户信息");
        mntmNewMenuItem_4.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminUserInfo();
            }
        });
        menu1.add(mntmNewMenuItem_4);

        JMenuItem mntmNewMenuItem_5 = new JMenuItem("借阅信息");
        mntmNewMenuItem_5.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBorrowInfo();
            }
        });
        menu1.add(mntmNewMenuItem_5);

        JMenu mnNewMenu_1 = new JMenu("退出系统");
        mnNewMenu_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                JOptionPane.showMessageDialog(null, "欢迎再次使用");
                jf.dispose();
            }
        });
        menuBar.add(mnNewMenu_1);


        jf.setVisible(true);
        jf.setResizable(true);
    }

    // 清空数据
    public void reset() {
        textField.setText("");
        textField_1.setText("");
        textField_2.setText("");
        textField_3.setText("");
        textField_4.setText("");
        textField_6.setText("");

    }

    public void getBookType() {

        // 获取连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet list = bookTypeDao.list(con, new BookType());
            while (list.next()) {
                BookType bookType = new BookType();
                bookType.setTypeId(list.getInt("id"));
                bookType.setTypeName(list.getString("type_name"));
                comboBox.addItem(bookType);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }


    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new AdminBookAdd();
    }
}
```





### 9.3 图书信息的修改 



```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

import javax.swing.JFrame;

import com.hechaodong.bookmanager.dao.BookTypeDao;
import com.hechaodong.bookmanager.model.BookType;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import com.hechaodong.bookmanager.dao.BookDao;
import com.hechaodong.bookmanager.model.Book;

import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;

import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.border.TitledBorder;
import javax.swing.table.DefaultTableModel;

import java.awt.Color;

import javax.swing.JLabel;
import javax.swing.JComboBox;

import java.awt.Font;
import java.math.BigDecimal;
import java.sql.ResultSet;
import java.util.Vector;

import javax.swing.JTextField;
import javax.swing.JButton;
import javax.swing.UIManager;

import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.ImageIcon;

public class AdminBookEdit extends JFrame {

    private JFrame jf;
    private JTextField textField;
    private JTable table;
    private DefaultTableModel model;
    private JTextField textField_1;
    private JTextField textField_2;
    private JTextField textField_3;
    private JTextField textField_4;
    private JTextField textField_5;
    private JTextField textField_6;
    private JTextField textField_7;

    private JComboBox comboBox;
    private JComboBox comboBox_1;
    private JComboBox comboBox_2;

    private DbUtil dbUtil = new DbUtil();
    private BookDao bookDao = new BookDao();
    private BookTypeDao bookTypeDao = new BookTypeDao();

    public AdminBookEdit() {

        // 初始化书籍修改界面
        jf = new JFrame("书籍修改");
        jf.setBounds(650, 250, 600, 672);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // 初始化菜单栏
        JMenuBar menuBar = new JMenuBar();
        jf.setJMenuBar(menuBar);

        // 类别管理
        JMenu mnNewMenu = new JMenu("类别管理");
        menuBar.add(mnNewMenu);

        JMenuItem mntmNewMenuItem = new JMenuItem("类别添加");
        mntmNewMenuItem.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminMenuFrm();
            }
        });
        mnNewMenu.add(mntmNewMenuItem);

        JMenuItem mntmNewMenuItem_1 = new JMenuItem("类别修改");
        mntmNewMenuItem_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBTypeEdit();
            }
        });
        mnNewMenu.add(mntmNewMenuItem_1);


        // 书籍管理
        JMenu mnNewMenu_2 = new JMenu("书籍管理");
        menuBar.add(mnNewMenu_2);

        JMenuItem mntmNewMenuItem_2 = new JMenuItem("书籍添加");
        mntmNewMenuItem_2.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookAdd();
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_2);

        JMenuItem mntmNewMenuItem_3 = new JMenuItem("书籍修改");
        mnNewMenu_2.add(mntmNewMenuItem_3);

        // 用户管理
        JMenu menu1 = new JMenu("用户管理");
        menuBar.add(menu1);

        JMenuItem mntmNewMenuItem_4 = new JMenuItem("用户信息");
        mntmNewMenuItem_4.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminUserInfo();
            }
        });
        menu1.add(mntmNewMenuItem_4);

        JMenuItem mntmNewMenuItem_5 = new JMenuItem("借阅信息");
        mntmNewMenuItem_5.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBorrowInfo();
            }
        });
        menu1.add(mntmNewMenuItem_5);


        // 退出系统
        JMenu mnNewMenu_1 = new JMenu("退出系统");
        mnNewMenu_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                JOptionPane.showMessageDialog(null, "欢迎再次使用");
                jf.dispose();
            }
        });
        menuBar.add(mnNewMenu_1);
        jf.getContentPane().setLayout(null);

        // 顶部展示“书目查询”的JLabel
        JPanel panel = new JPanel();
        panel.setBorder(new TitledBorder(null, "书目查询", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel.setBounds(20, 10, 541, 78);
        jf.getContentPane().add(panel);
        panel.setLayout(null);

        // 下拉框选项
        comboBox = new JComboBox();
        comboBox.setFont(new Font("幼圆", Font.BOLD, 15));
        comboBox.setBounds(55, 28, 109, 24);
        comboBox.addItem("书籍名称");
        comboBox.addItem("书籍作者");
        panel.add(comboBox);

        // 初始化查询所对应的文本框
        textField = new JTextField();
        textField.setBounds(185, 28, 146, 24);
        panel.add(textField);
        textField.setColumns(10);

        // 查询按钮
        JButton btnNewButton = new JButton("查询");
        btnNewButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int index = comboBox.getSelectedIndex();
                if (index == 0) {
                    String bookName = textField.getText();
                    Book book = new Book();
                    book.setBookName(bookName);
                    putDates(book);
                } else {
                    String authoerName = textField.getText();
                    Book book = new Book();
                    book.setAuthor(authoerName);
                    putDates(book);
                }
            }
        });
        btnNewButton.setFont(new Font("幼圆", Font.BOLD, 14));
        btnNewButton.setBounds(352, 28, 81, 25);
        panel.add(btnNewButton);


        // 中部展示“书籍信息”的JLabel
        JPanel panel_1 = new JPanel();
        panel_1.setLayout(null);
        panel_1.setBorder(new TitledBorder(UIManager.getBorder("TitledBorder.border"), "书籍信息", TitledBorder.LEADING, TitledBorder.TOP, null, new Color(255, 0, 0)));
        panel_1.setBounds(20, 105, 541, 195);

        // 表头栏数据  一位数组
        String[] title = {"编号", "书名", "类别", "作者", "价格", "库存", "状态"};
        // 具体的各栏行记录 先用空的二位数组占位
        String[][] dates = {};

        // 创建数据模型，实例化上面2个控件对象
        model = new DefaultTableModel(dates, title);
        table = new JTable(model);

        // 获取数据库数据放置table中
        putDates(new Book());
        panel_1.setLayout(null);
        JScrollPane jscrollpane = new JScrollPane();
        jscrollpane.setBounds(20, 22, 496, 154);
        jscrollpane.setViewportView(table);
        panel_1.add(jscrollpane);
        jf.getContentPane().add(panel_1);

        // 给表格添加一个鼠标监听器
        table.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                tableMousePressed(evt);
            }
        });

        // 创建一个Panel对象
        JPanel panel_2 = new JPanel();
        panel_2.setBounds(20, 310, 541, 292);
        jf.getContentPane().add(panel_2);
        panel_2.setLayout(null);

        // 初始化展示“编号”的JLabel
        JLabel label = new JLabel("编号：");
        label.setFont(new Font("幼圆", Font.BOLD, 14));
        label.setBounds(58, 10, 45, 27);
        panel_2.add(label);

        // 初始化输入编号的文本框组件
        textField_1 = new JTextField();
        textField_1.setColumns(10);
        textField_1.setBounds(101, 10, 129, 27);
        panel_2.add(textField_1);

        // 初始化展示“书名”的JLabel
        JLabel label_1 = new JLabel("书名：");
        label_1.setFont(new Font("幼圆", Font.BOLD, 14));
        label_1.setBounds(294, 10, 45, 27);
        panel_2.add(label_1);

        // 初始化输入书名的文本框组件
        textField_2 = new JTextField();
        textField_2.setColumns(10);
        textField_2.setBounds(338, 10, 128, 27);
        panel_2.add(textField_2);

        // 初始化展示“作者”的JLabel
        JLabel label_2 = new JLabel("作者：");
        label_2.setFont(new Font("幼圆", Font.BOLD, 14));
        label_2.setBounds(58, 58, 45, 27);
        panel_2.add(label_2);

        // 初始化输入作者的文本框组件
        textField_3 = new JTextField();
        textField_3.setColumns(10);
        textField_3.setBounds(101, 58, 129, 27);
        panel_2.add(textField_3);

        // 价格 JLabel
        JLabel label_3 = new JLabel("价格：");
        label_3.setFont(new Font("幼圆", Font.BOLD, 14));
        label_3.setBounds(58, 104, 45, 27);
        panel_2.add(label_3);

        textField_4 = new JTextField();
        textField_4.setColumns(10);
        textField_4.setBounds(101, 104, 129, 27);
        panel_2.add(textField_4);

        // 出版 JLabel
        JLabel label_4 = new JLabel("出版：");
        label_4.setFont(new Font("幼圆", Font.BOLD, 14));
        label_4.setBounds(294, 58, 45, 27);
        panel_2.add(label_4);

        textField_5 = new JTextField();
        textField_5.setColumns(10);
        textField_5.setBounds(337, 58, 129, 27);
        panel_2.add(textField_5);

        // 类别 JLabel
        JLabel label_5 = new JLabel("类别：");
        label_5.setFont(new Font("幼圆", Font.BOLD, 14));
        label_5.setBounds(58, 189, 45, 27);
        panel_2.add(label_5);

        // “类别”下拉选择框
        comboBox_1 = new JComboBox();
        comboBox_1.setBounds(102, 190, 128, 26);

        //获取类别
        getBookType();
        panel_2.add(comboBox_1);


        // 库存 JLabel
        JLabel label_6 = new JLabel("库存：");
        label_6.setFont(new Font("幼圆", Font.BOLD, 14));
        label_6.setBounds(294, 104, 45, 27);
        panel_2.add(label_6);

        textField_6 = new JTextField();
        textField_6.setColumns(10);
        textField_6.setBounds(337, 104, 129, 27);
        panel_2.add(textField_6);

        // 描述 JLabel
        JLabel label_7 = new JLabel("描述：");
        label_7.setFont(new Font("幼圆", Font.BOLD, 14));
        label_7.setBounds(58, 152, 45, 27);
        panel_2.add(label_7);

        textField_7 = new JTextField();
        textField_7.setColumns(10);
        textField_7.setBounds(101, 152, 365, 27);
        panel_2.add(textField_7);


        // 状态 JLabel
        JLabel label_8 = new JLabel("状态：");
        label_8.setFont(new Font("幼圆", Font.BOLD, 14));
        label_8.setBounds(294, 190, 45, 27);
        panel_2.add(label_8);

        comboBox_2 = new JComboBox();
        comboBox_2.setBounds(338, 191, 128, 26);
        comboBox_2.addItem("上架");
        comboBox_2.addItem("下架");
        panel_2.add(comboBox_2);

		// 修改按钮
        JButton btnNewButton_1 = new JButton("修改");
        btnNewButton_1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                // 获取文本框组件中的相关数据
                String bookName = textField_2.getText();
                String author = textField_3.getText();
                String priceStr = textField_4.getText();
                String publish = textField_5.getText();
                String numberStr = textField_6.getText();
                String remark = textField_7.getText();
                String bookId = textField_1.getText();

                // 对数据进行校验
                if (ToolUtil.isEmpty(bookId) || ToolUtil.isEmpty(bookName)
                        || ToolUtil.isEmpty(author) || ToolUtil.isEmpty(publish)
                        || ToolUtil.isEmpty(priceStr)
                        || ToolUtil.isEmpty(numberStr) || ToolUtil.isEmpty(remark)) {
                    JOptionPane.showMessageDialog(null, "请输入相关内容");
                    return;
                }

                // 获取图书的类别数据
                BookType bookType = (BookType) comboBox_1.getSelectedItem();
                Integer typeId = bookType.getTypeId();

                int index = comboBox_2.getSelectedIndex();

                // 对库存数据价格数据进行处理
                int number;
                double price;
                try {
                    number = Integer.parseInt(numberStr);
                    price = new BigDecimal(priceStr).setScale(2, BigDecimal.ROUND_DOWN).doubleValue();
                } catch (Exception e1) {
                    JOptionPane.showMessageDialog(null, "参数错误");
                    return;
                }

                // 创建Book对象进行数据封装
                Book book = new Book();
                book.setBookId(Integer.parseInt(bookId));
                book.setBookName(bookName);
                book.setAuthor(author);
                book.setBookTypeId(typeId);
                book.setNumber(number);
                book.setPrice(price);
                book.setPublish(publish);
                book.setRemark(remark);
                book.setStatus(1);
                // 判断上架下架状态
                if (index == 0) {
                    book.setStatus(1);
                } else if (index == 1) {
                    book.setStatus(2);
                }

                // 获取连接对象
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    int i = bookDao.update(con, book);

                    // 判断
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "修改成功");
                        putDates(new Book()); //+++++++
                    } else {
                        JOptionPane.showMessageDialog(null, "修改失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "修改异常");
                } finally {
                    try {
                        dbUtil.closeCon(con);
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }

                putDates(new Book());
            }
        });
        // 修改按钮
        btnNewButton_1.setFont(new Font("幼圆", Font.BOLD, 14));
        btnNewButton_1.setBounds(304, 235, 93, 35);
        panel_2.add(btnNewButton_1);

        // 背景图片
        JLabel lblNewLabel = new JLabel("");
        lblNewLabel.setIcon(new ImageIcon("lib/images/5.png"));
        lblNewLabel.setBounds(0, 0, 584, 613);
        jf.getContentPane().add(lblNewLabel);

        jf.setVisible(true);
        jf.setResizable(true);
    }

    // 获取图书类型
    public void getBookType() {

        // 获取连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet list = bookTypeDao.list(con, new BookType());
            while (list.next()) {
                BookType bookType = new BookType();
                bookType.setTypeId(list.getInt("id"));
                bookType.setTypeName(list.getString("type_name"));
                System.out.println(bookType);
                /*
                 * 添加图书中类别设置
                 * */
                comboBox_1.addItem(bookType);
//                comboBox_1.addItem(String.valueOf(bookType.getTypeName()));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    //点击表格获取数据
    public void tableMousePressed(MouseEvent evt) {
        int row = table.getSelectedRow();
        Integer bookId = (Integer) table.getValueAt(row, 0);
        Book book = new Book();
        book.setBookId(bookId);

        // 获取连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet list = bookDao.list(con, book);
            if (list.next()) {
                textField_1.setText(list.getString("id"));
                textField_2.setText(list.getString("book_name"));
                textField_3.setText(list.getString("author"));
                textField_5.setText(list.getString("publish"));
                textField_4.setText(list.getString("price"));
                textField_6.setText(list.getString("number"));
                textField_7.setText(list.getString("remark"));
                int status = list.getInt("status");
                if (status == 1) {
                    comboBox_2.setSelectedIndex(0);
                } else {
                    comboBox_2.setSelectedIndex(1);
                }
                int typeId = list.getInt("type_id");
                int count = comboBox_1.getItemCount();
                for (int i = 0; i < count; i++) {
                    BookType bookType = (BookType) comboBox_1.getItemAt(i);
                    if (bookType.getTypeId() == typeId) {
                        comboBox_1.setSelectedIndex(i);
                    }
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    // 从数据库中获取数据
    private void putDates(Book book) {
        DefaultTableModel model = (DefaultTableModel) table.getModel();
        model.setRowCount(0);
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet resultSet = bookDao.list(con, book);
            while (resultSet.next()) {
                Vector rowData = new Vector();
                rowData.add(resultSet.getInt("id"));
                rowData.add(resultSet.getString("book_name"));
                rowData.add(resultSet.getString("type_name"));
                rowData.add(resultSet.getString("author"));
                rowData.add(resultSet.getDouble("price"));
                rowData.add(resultSet.getInt("number"));
                if (resultSet.getInt("status") == 1) {
                    rowData.add("上架");
                } else {
                    rowData.add("下架");
                }
                model.addRow(rowData);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new AdminBookEdit();
    }
}

```





### 9.4 图书类型的修改



```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.Color;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.sql.ResultSet;
import java.util.Vector;

import javax.swing.JFrame;

import com.hechaodong.bookmanager.dao.BookTypeDao;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import com.hechaodong.bookmanager.model.BookType;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;

import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.UIManager;
import javax.swing.border.TitledBorder;
import javax.swing.table.DefaultTableModel;
import javax.swing.JLabel;

import java.awt.Font;

import javax.swing.JTextField;
import javax.swing.JButton;

import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.ImageIcon;

public class AdminBTypeEdit extends JFrame {
    private JFrame jf;
    private JTable table;
    private DefaultTableModel model;
    private JTextField textField;
    private JTextField textField_1;
    private JTextField textField_2;

    private DbUtil dbUtil = new DbUtil();
    private BookTypeDao bookTypeDao = new BookTypeDao();

    public AdminBTypeEdit() {

        // 初始化类别修改界面
        jf = new JFrame("类别修改");
        jf.setBounds(650, 250, 611, 472);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        JMenuBar menuBar = new JMenuBar();
        jf.setJMenuBar(menuBar);

        JMenu mnNewMenu = new JMenu("类别管理");
        menuBar.add(mnNewMenu);

        JMenuItem mntmNewMenuItem = new JMenuItem("类别添加");
        mntmNewMenuItem.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminMenuFrm();
            }
        });
        mnNewMenu.add(mntmNewMenuItem);

        JMenuItem mntmNewMenuItem_1 = new JMenuItem("类别修改");
        mnNewMenu.add(mntmNewMenuItem_1);

        JMenu mnNewMenu_2 = new JMenu("书籍管理");
        menuBar.add(mnNewMenu_2);

        JMenuItem mntmNewMenuItem_2 = new JMenuItem("书籍添加");
        mntmNewMenuItem_2.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookAdd();
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_2);

        JMenuItem mntmNewMenuItem_3 = new JMenuItem("书籍修改");
        mntmNewMenuItem_3.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookEdit();
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_3);

        JMenu menu1 = new JMenu("用户管理");
        menuBar.add(menu1);

        JMenuItem mntmNewMenuItem_4 = new JMenuItem("用户信息");
        mntmNewMenuItem_4.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminUserInfo();
            }
        });
        menu1.add(mntmNewMenuItem_4);

        JMenuItem mntmNewMenuItem_5 = new JMenuItem("借阅信息");
        mntmNewMenuItem_5.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBorrowInfo();
            }
        });
        menu1.add(mntmNewMenuItem_5);

        JMenu mnNewMenu_1 = new JMenu("退出系统");
        mnNewMenu_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                JOptionPane.showMessageDialog(null, "欢迎再次使用");
                jf.dispose();
            }
        });
        menuBar.add(mnNewMenu_1);

        // 顶部展示“类别信息”的JLabel
        JPanel panel_1 = new JPanel();
        panel_1.setBorder(new TitledBorder(UIManager.getBorder("TitledBorder.border"), "类别信息", TitledBorder.LEADING, TitledBorder.TOP, null, new Color(255, 0, 0)));
        panel_1.setBounds(20, 10, 554, 208);

        // 表头栏数据
        String[] title = {"编号", "类别名称", "类别描述"};
        //具体的各栏行记录 先用空的二位数组占位
        String[][] dates = {};

        // 创建数据模型，实例化上面2个控件对象
        model = new DefaultTableModel(dates, title);
        table = new JTable(model);

        //获取数据库数据放置table中
        putDates();
        panel_1.setLayout(null);
        JScrollPane jscrollpane = new JScrollPane();
        jscrollpane.setBounds(20, 22, 517, 163);
        jscrollpane.setViewportView(table);
        panel_1.add(jscrollpane);
        jf.getContentPane().add(panel_1);

        // 底部展示“类别编辑”的JLabel
        JPanel panel = new JPanel();
        panel.setBorder(new TitledBorder(null, "类别编辑", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel.setBounds(20, 228, 554, 168);
        jf.getContentPane().add(panel);
        panel.setLayout(null);

        table.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                typeTableMousePressed(evt);
            }
        });

        // 编号 JLabel
        JLabel lblNewLabel = new JLabel("编号：");
        lblNewLabel.setFont(new Font("幼圆", Font.BOLD, 14));
        lblNewLabel.setBounds(73, 26, 45, 28);
        panel.add(lblNewLabel);

        // 编号 文本框
        textField = new JTextField();
        textField.setBounds(116, 30, 92, 24);
        panel.add(textField);
        textField.setColumns(10);

        // 类别名称 JLabel
        JLabel label = new JLabel("类别名称：");
        label.setFont(new Font("幼圆", Font.BOLD, 14));
        label.setBounds(238, 26, 75, 28);
        panel.add(label);

        // 类别名称 文本框
        textField_1 = new JTextField();
        textField_1.setColumns(10);
        textField_1.setBounds(314, 30, 122, 24);
        panel.add(textField_1);

        // 描述 JLabel
        JLabel label_1 = new JLabel("描述：");
        label_1.setFont(new Font("幼圆", Font.BOLD, 14));
        label_1.setBounds(73, 65, 45, 28);
        panel.add(label_1);

        // 描述 文本框
        textField_2 = new JTextField();
        textField_2.setColumns(10);
        textField_2.setBounds(116, 69, 320, 24);
        panel.add(textField_2);

        // 修改按钮
        JButton btnNewButton = new JButton("修改");
        // 给修改按钮添加一个事件监听器
        btnNewButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                // 获取信息
                String typeId = textField.getText();
                String typeName = textField_1.getText();
                String typeRemark = textField_2.getText();
                if (ToolUtil.isEmpty(typeName) || ToolUtil.isEmpty(typeRemark)) {
                    JOptionPane.showMessageDialog(null, "请输入相关信息");
                    return;
                }
                // 封装数据BookType
                BookType bookType = new BookType();
                bookType.setTypeId(Integer.parseInt(typeId));
                bookType.setTypeName(typeName);
                bookType.setRemark(typeRemark);
                // 获取连接对象
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    int i = bookTypeDao.update(con, bookType);
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "修改成功");
                        putDates();
                    } else {
                        JOptionPane.showMessageDialog(null, "修改失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "修改异常");
                } finally {
                    try {
                        dbUtil.closeCon(con);
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }
            }
        });
        btnNewButton.setFont(new Font("幼圆", Font.BOLD, 14));
        btnNewButton.setBounds(128, 117, 93, 28);
        panel.add(btnNewButton);

        // 删除按钮
        JButton button = new JButton("删除");

        // 给删除按钮添加事件监听器
        button.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                // 获取数据
                String typeId = textField.getText();
                if (ToolUtil.isEmpty(typeId)) {
                    JOptionPane.showMessageDialog(null, "请选择相关信息");
                    return;
                }
                // 获取连接对象
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    int i = bookTypeDao.delete(con, typeId);
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "删除成功");
                        putDates();
                    } else if (i == 2) {
                        JOptionPane.showMessageDialog(null, "删除失败-类别最少保留一个");
                    } else if (i == 3) {
                        JOptionPane.showMessageDialog(null, "删除失败-该类别下有书籍");
                    } else {
                        JOptionPane.showMessageDialog(null, "删除失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "删除异常");
                } finally {
                    try {
                        dbUtil.closeCon(con);
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }
            }
        });
        button.setFont(new Font("幼圆", Font.BOLD, 14));
        button.setBounds(314, 117, 93, 28);
        panel.add(button);

        // 背景图片
        JLabel lblNewLabel_1 = new JLabel("");
        lblNewLabel_1.setIcon(new ImageIcon("lib/images/5.png"));
        lblNewLabel_1.setBounds(0, 0, 595, 413);
        jf.getContentPane().add(lblNewLabel_1);

        // 显示
        jf.setVisible(true);
        jf.setResizable(false);
    }

    // 点击表格获取信息
    protected void typeTableMousePressed(MouseEvent evt) {
        int row = table.getSelectedRow();
        textField.setText(table.getValueAt(row, 0).toString());
        textField_1.setText(table.getValueAt(row, 1).toString());
        textField_2.setText(table.getValueAt(row, 2).toString());

    }

    // 将图书类型信息显示在表格中
    public void putDates() {
        DefaultTableModel model = (DefaultTableModel) table.getModel();
        model.setRowCount(0);
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet list = bookTypeDao.list(con, new BookType());
            while (list.next()) { // 遍历"list"对象中的每一行数据，将其转换为一个Vector对象
                Vector rowData = new Vector();
                rowData.add(list.getInt("id"));
                rowData.add(list.getString("type_name"));
                rowData.add(list.getString("remark"));
                model.addRow(rowData);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new AdminBTypeEdit();
    }
}

```







## 10. 用户管理模块



### 10.1 用户信息



```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

import javax.swing.JFrame;

import com.hechaodong.bookmanager.dao.UserDao;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import com.hechaodong.bookmanager.model.User;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;

import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.UIManager;
import javax.swing.border.TitledBorder;
import javax.swing.table.DefaultTableModel;

import java.awt.Color;

import javax.swing.JLabel;

import java.awt.Font;
import java.sql.ResultSet;
import java.util.Vector;

import javax.swing.JTextField;
import javax.swing.JButton;

import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import javax.swing.ImageIcon;

// 用户信息
public class AdminUserInfo extends JFrame {
    private JFrame jf;
    private JTextField textField;
    private JTable table;
    private DefaultTableModel model;
    private JTextField textField_1;
    private JTextField textField_2;
    private JTextField textField_3;
    private JTextField textField_4;
    private JTextField textField_5;

    private DbUtil dbUtil = new DbUtil();
    private UserDao userDao = new UserDao();

    public AdminUserInfo() {
        // 初始化用户信息界面
        jf = new JFrame("用户信息");
        jf.setBounds(650, 250, 600, 516);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        // 创建一个菜单栏
        JMenuBar menuBar = new JMenuBar();
        jf.setJMenuBar(menuBar);

        JMenu mnNewMenu = new JMenu("类别管理");
        menuBar.add(mnNewMenu);

        JMenuItem mntmNewMenuItem = new JMenuItem("类别添加");
        mntmNewMenuItem.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminMenuFrm();// 类别添加（默认主界面）
            }
        });
        mnNewMenu.add(mntmNewMenuItem);

        JMenuItem mntmNewMenuItem_1 = new JMenuItem("类别修改");
        mntmNewMenuItem_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBTypeEdit();// 类别修改
            }
        });
        mnNewMenu.add(mntmNewMenuItem_1);

        JMenu mnNewMenu_2 = new JMenu("书籍管理");
        menuBar.add(mnNewMenu_2);

        JMenuItem mntmNewMenuItem_2 = new JMenuItem("书籍添加");
        mntmNewMenuItem_2.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookAdd();// 书籍添加
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_2);

        JMenuItem mntmNewMenuItem_3 = new JMenuItem("书籍修改");
        mntmNewMenuItem_3.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookEdit();// 书籍修改
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_3);

        JMenu menu1 = new JMenu("用户管理");
        menuBar.add(menu1);

        JMenuItem mntmNewMenuItem_4 = new JMenuItem("用户信息");
        menu1.add(mntmNewMenuItem_4);

        JMenuItem mntmNewMenuItem_5 = new JMenuItem("借阅信息");
        mntmNewMenuItem_5.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBorrowInfo();// 借阅信息
            }
        });
        menu1.add(mntmNewMenuItem_5);

        JMenu mnNewMenu_1 = new JMenu("退出系统");
        mnNewMenu_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                JOptionPane.showMessageDialog(null, "欢迎再次使用");
                jf.dispose();
            }
        });
        menuBar.add(mnNewMenu_1);

        // 顶部展示“借阅信息”的JLabel
        JPanel panel = new JPanel();
        panel.setBorder(new TitledBorder(null, "借阅信息", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel.setBounds(20, 10, 540, 74);
        jf.getContentPane().add(panel);
        panel.setLayout(null);

        // 初始化展示“用户名”的JLabel
        JLabel lblNewLabel = new JLabel("用户名：");
        lblNewLabel.setFont(new Font("幼圆", Font.BOLD, 14));
        lblNewLabel.setBounds(57, 22, 60, 30);
        panel.add(lblNewLabel);

        // 初始化用户名所对应的文本框组件
        textField = new JTextField();
        textField.setBounds(127, 27, 155, 25);
        panel.add(textField);
        textField.setColumns(10);

        // 查询按钮
        JButton btnNewButton = new JButton("查询");
        btnNewButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String userName = textField.getText();// 获取查询信息
                User user = new User();
                user.setUserName(userName);
                putDates(user);
            }
        });
        btnNewButton.setFont(new Font("幼圆", Font.BOLD, 14));
        btnNewButton.setBounds(316, 26, 93, 23);
        panel.add(btnNewButton);

        // 中部展示”用户信息“的JLabel
        JPanel panel_1 = new JPanel();
        panel_1.setLayout(null);
        panel_1.setBorder(new TitledBorder(UIManager.getBorder("TitledBorder.border"), "用户信息", TitledBorder.LEADING, TitledBorder.TOP, null, new Color(255, 0, 0)));
        panel_1.setBounds(20, 94, 541, 195);

        // 表头栏数据
        String[] title = {"编号", "用户名", "密码", "性别", "电话"};
        // 具体的各栏行记录 先用空的二位数组占位
        String[][] dates = {};

        //创建数据模型，实例化上面2个控件对象
        model = new DefaultTableModel(dates, title);
        table = new JTable(model);

        //获取数据库数据放置table中
        putDates(new User());

		// 创建JScrollPanel对象
        panel_1.setLayout(null);
        JScrollPane jscrollpane = new JScrollPane();
        jscrollpane.setBounds(20, 22, 496, 154);
        jscrollpane.setViewportView(table);
        panel_1.add(jscrollpane);
        jf.getContentPane().add(panel_1);

		// 底部展示“用户编辑”的JLabel
        JPanel panel_2 = new JPanel();
        panel_2.setBorder(new TitledBorder(null, "用户编辑", TitledBorder.LEADING, TitledBorder.TOP, null, Color.RED));
        panel_2.setBounds(20, 302, 540, 137);
        jf.getContentPane().add(panel_2);
        panel_2.setLayout(null);

		// 编号 JLabel
        JLabel lblNewLabel_1 = new JLabel("编号：");
        lblNewLabel_1.setFont(new Font("幼圆", Font.BOLD, 15));
        lblNewLabel_1.setBounds(49, 30, 48, 34);
        panel_2.add(lblNewLabel_1);

		// 编号 文本框
        textField_1 = new JTextField();
        textField_1.setEditable(false);
        textField_1.setBounds(103, 37, 66, 21);
        panel_2.add(textField_1);
        textField_1.setColumns(10);

		// 用户名 JLabel
        JLabel label = new JLabel("用户名：");
        label.setFont(new Font("幼圆", Font.BOLD, 15));
        label.setBounds(187, 30, 66, 34);
        panel_2.add(label);

		// 用户名 文本框
        textField_2 = new JTextField();
        textField_2.setColumns(10);
        textField_2.setBounds(259, 37, 93, 21);
        panel_2.add(textField_2);

		// 密码 JLabel
        JLabel label_1 = new JLabel("密码：");
        label_1.setFont(new Font("幼圆", Font.BOLD, 15));
        label_1.setBounds(383, 30, 48, 34);
        panel_2.add(label_1);

		// 密码 文本框
        textField_3 = new JTextField();
        textField_3.setColumns(10);
        textField_3.setBounds(437, 37, 93, 21);
        panel_2.add(textField_3);

		// 修改按钮
        JButton btnNewButton_1 = new JButton("修改");

		// 给修改按钮添加一个事件监听器
        btnNewButton_1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
				// 获取数据
                String userId = textField_1.getText();
                String userName = textField_2.getText();
                String password = textField_3.getText();
                String sex = textField_4.getText();
                String phone = textField_5.getText();
                if (ToolUtil.isEmpty(userName)
                        || ToolUtil.isEmpty(password)
                        || ToolUtil.isEmpty(sex) || ToolUtil.isEmpty(phone)) {
                    JOptionPane.showMessageDialog(null, "请输入相关信息");
                    return;
                }
				// 把数据封装到User中
                User user = new User();
                user.setUserId(Integer.parseInt(userId));
                user.setUserName(userName);
                user.setPassword(password);
                user.setSex(sex);
                user.setPhone(phone);
				// 获取连接对象
                Connection con = null;
                try {
                    con = dbUtil.getConnection();
                    int i = userDao.update(con, user);
                    if (i == 1) {
                        JOptionPane.showMessageDialog(null, "修改成功");
                        putDates(new User());
                    } else {
                        JOptionPane.showMessageDialog(null, "修改失败");
                    }
                } catch (Exception e1) {
                    e1.printStackTrace();
                    JOptionPane.showMessageDialog(null, "修改异常");
                } finally {
                    try {
                        dbUtil.closeCon(con);
                    } catch (Exception e1) {
                        e1.printStackTrace();
                    }
                }
            }
        });
        btnNewButton_1.setFont(new Font("幼圆", Font.BOLD, 15));
        btnNewButton_1.setBounds(422, 74, 87, 34);
        panel_2.add(btnNewButton_1);

		// 性别 JLabel
        JLabel label_2 = new JLabel("性别：");
        label_2.setFont(new Font("幼圆", Font.BOLD, 15));
        label_2.setBounds(49, 74, 48, 34);
        panel_2.add(label_2);

		// 性别 文本框
        textField_4 = new JTextField();
        textField_4.setColumns(10);
        textField_4.setBounds(103, 81, 66, 21);
        panel_2.add(textField_4);

		// 手机号 JLabel
        JLabel label_3 = new JLabel("手机号：");
        label_3.setFont(new Font("幼圆", Font.BOLD, 15));
        label_3.setBounds(187, 74, 66, 34);
        panel_2.add(label_3);

		// 手机号 文本框
        textField_5 = new JTextField();
        textField_5.setColumns(10);
        textField_5.setBounds(259, 81, 93, 21);
        panel_2.add(textField_5);

		// 背景图片
        JLabel lblNewLabel_2 = new JLabel("");
        lblNewLabel_2.setIcon(new ImageIcon("lib/images/5.png"));
        lblNewLabel_2.setBounds(0, 0, 584, 457);
        jf.getContentPane().add(lblNewLabel_2);

        table.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                tableMousePressed(evt);
            }
        });

		// 显示，不改变界面大小
        jf.setVisible(true);
        jf.setResizable(false);
    }

    public void tableMousePressed(MouseEvent evt) {
        int row = table.getSelectedRow();
        textField_1.setText(table.getValueAt(row, 0).toString());
        textField_2.setText(table.getValueAt(row, 1).toString());
        textField_3.setText(table.getValueAt(row, 2).toString());
        textField_4.setText(table.getValueAt(row, 3).toString());
        textField_5.setText(table.getValueAt(row, 4).toString());
    }

    public void putDates(User user) {
        DefaultTableModel model = (DefaultTableModel) table.getModel();
        model.setRowCount(0);
		// 获取连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet list = userDao.list(con, user);
            while (list.next()) {
                Vector rowData = new Vector();
                rowData.add(list.getInt("id"));
                rowData.add(list.getString("username"));
                rowData.add(list.getString("password"));
                rowData.add(list.getString("sex"));
                rowData.add(list.getString("phone"));
                model.addRow(rowData);
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new AdminUserInfo();
    }
}

```





### 10.2 借阅信息

```java
package com.hechaodong.bookmanager.jframe;

import java.sql.*;
import java.awt.Color;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.sql.ResultSet;
import java.util.Vector;

import javax.swing.JFrame;

import com.hechaodong.bookmanager.dao.BorrowDetailDao;
import com.hechaodong.bookmanager.model.BorrowDetail;
import com.hechaodong.bookmanager.utils.DbUtil;
import com.hechaodong.bookmanager.utils.ToolUtil;
import org.jb2011.lnf.beautyeye.BeautyEyeLNFHelper;

import javax.swing.JMenuBar;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.UIManager;
import javax.swing.border.TitledBorder;
import javax.swing.table.DefaultTableModel;
import javax.swing.JLabel;
import javax.swing.ImageIcon;

public class AdminBorrowInfo extends JFrame {
    private JFrame jf;
    private JTable table;
    private DefaultTableModel model;

    private DbUtil dbUtil = new DbUtil();
    private BorrowDetailDao borrowDetailDao = new BorrowDetailDao();

    public AdminBorrowInfo() {

        // 初始化借阅信息界面
        jf = new JFrame("借阅信息");
        jf.setBounds(650, 250, 610, 441);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.getContentPane().setLayout(null);

        // 创建菜单栏
        JMenuBar menuBar = new JMenuBar();
        jf.setJMenuBar(menuBar);

        JMenu mnNewMenu = new JMenu("类别管理");
        menuBar.add(mnNewMenu);

        JMenuItem mntmNewMenuItem = new JMenuItem("类别添加");
        mntmNewMenuItem.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminMenuFrm();
            }
        });
        mnNewMenu.add(mntmNewMenuItem);

        JMenuItem mntmNewMenuItem_1 = new JMenuItem("类别修改");
        mntmNewMenuItem_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBTypeEdit();
            }
        });
        mnNewMenu.add(mntmNewMenuItem_1);

        JMenu mnNewMenu_2 = new JMenu("书籍管理");
        menuBar.add(mnNewMenu_2);

        JMenuItem mntmNewMenuItem_2 = new JMenuItem("书籍添加");
        mntmNewMenuItem_2.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookAdd();
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_2);

        JMenuItem mntmNewMenuItem_3 = new JMenuItem("书籍修改");
        mntmNewMenuItem_3.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminBookEdit();
            }
        });
        mnNewMenu_2.add(mntmNewMenuItem_3);

        JMenu menu1 = new JMenu("用户管理");
        menuBar.add(menu1);

        JMenuItem mntmNewMenuItem_4 = new JMenuItem("用户信息");
        mntmNewMenuItem_4.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                jf.dispose();
                new AdminUserInfo();
            }
        });
        menu1.add(mntmNewMenuItem_4);

        JMenuItem mntmNewMenuItem_5 = new JMenuItem("借阅信息");
        menu1.add(mntmNewMenuItem_5);

        JMenu mnNewMenu_1 = new JMenu("退出系统");
        mnNewMenu_1.addMouseListener(new MouseAdapter() {
            public void mousePressed(MouseEvent evt) {
                JOptionPane.showMessageDialog(null, "欢迎再次使用");
                jf.dispose();
            }
        });
        menuBar.add(mnNewMenu_1);

        // 顶部“借阅信息”的JLabel
        JPanel panel_1 = new JPanel();
        panel_1.setBorder(new TitledBorder(UIManager.getBorder("TitledBorder.border"), "借阅信息", TitledBorder.LEADING, TitledBorder.TOP, null, new Color(255, 0, 0)));
        panel_1.setBounds(10, 10, 574, 350);

        // 表头栏数据
        String[] title = {"借书人", "书名", "状态", "借书时间", "还书时间"};
        // 具体的各栏行记录 先用空的二位数组占位
        String[][] dates = {};

        // 创建数据模型，实例化上面2个控件对象*/
        model = new DefaultTableModel(dates, title);
        table = new JTable(model);

        //获取数据库数据放置table中
        putDates(new BorrowDetail());
        // 借阅信息表格
        panel_1.setLayout(null);
        JScrollPane jscrollpane = new JScrollPane();
        jscrollpane.setBounds(20, 22, 538, 314);
        jscrollpane.setViewportView(table);
        panel_1.add(jscrollpane);
        jf.getContentPane().add(panel_1);

        // 背景图片
        JLabel lblNewLabel = new JLabel("");
        lblNewLabel.setIcon(new ImageIcon("lib/images/6.png"));
        lblNewLabel.setBounds(0, 0, 584, 379);
        jf.getContentPane().add(lblNewLabel);

        // 显示
        jf.setVisible(true);
        jf.setResizable(true);
    }

    //
    private void putDates(BorrowDetail borrowDetail) {
        DefaultTableModel model = (DefaultTableModel) table.getModel();
        model.setRowCount(0);
        // 获取连接对象
        Connection con = null;
        try {
            con = dbUtil.getConnection();
            ResultSet list = borrowDetailDao.list(con, borrowDetail);
            while (list.next()) {
                Vector rowData = new Vector();
                rowData.add(list.getString("username"));
                rowData.add(list.getString("book_name"));
                int status = list.getInt("status");
                if (status == 1) {
                    rowData.add("在借");
                } else {
                    rowData.add("已还");
                }
                rowData.add(ToolUtil.getDateByTime(list.getLong("borrow_time")));
                if (status == 2) {
                    rowData.add(ToolUtil.getDateByTime(list.getLong("return_time")));
                }
                model.addRow(rowData);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                dbUtil.closeCon(con);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        try {
            BeautyEyeLNFHelper.frameBorderStyle = BeautyEyeLNFHelper.FrameBorderStyle.generalNoTranslucencyShadow;
            BeautyEyeLNFHelper.launchBeautyEyeLNF();
        } catch (Exception e) {
            e.printStackTrace();
        }
        new AdminBorrowInfo();
    }
}

```







