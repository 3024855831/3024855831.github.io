---
layout: post
title:  "mysql & pdo"
date:   2016-9-22 20:31:01 +0800
categories: 数据库
tag: 小记
---

* content
{:toc}

数据库是一个按照数据结构来组织、存储和管理数据的仓库。如：Mysql、Sql Server、Oracle等。在PHP中我们惯于用Mysql。

那既然我们使用的是Mysql数据库。有没有一个客户端来帮助我们更快速操作我们的数据库。Navicat是个不错的选择。

接下来我们来学习使用PHP来连接我们Mysql数据库。

<font face="STCAIYUN" color="red">第一种方法：使用mysqli来连接数据库</font>

    $con = mysqli_connect('127.0.0.1','root','root','test');
    mysqli_query('set name utf8',$con);
    $data = mysqli_query('selet * from user',$con);

需要注意的是`mysqli_connect()`有四个参数。第一个是你的IP，第二个是你Mysql的用户名，第三个是你Mysql的密码。第四个是要使用的数据库。
特别注意每次我们使用`mysql_query`第二个参数一定要带上上述`$con`

<font face="STCAIYUN" color="red">第二种方法：使用PDO来连接数据库</font>
PDO是我们PHP中的一个类。具体使用方法如下：
	
	try {
		//$dsn是数据源  
	    $dsn='mysql:host=localhost;dbname=test';  
	    $username='root';  
	    $passwd='root';  
	    $pdo=new PDO($dsn,$username,$passwd);  
	    //如果连接成功的话，得到的是pdo的对象  
		$dbh->query('set names utf8;');
		$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
		$dbh->commit();

	} catch (Exception $e) {
		$dbh->rollBack();
		echo “Failed: ” . $e->getMessage();
	}

现在你已经通过PDO建立了连接，在部署查询之前你必须搞明白PDO是怎样管理事务的。如果你以前从未遇到过事务处理，（现在简单介绍一下：）它们提供了4个主要的特性：<font color="red">原子性，一致性，独立性和持久性</font>（Atomicity, Consistency, Isolation and Durability，ACID）通俗一点讲，一个事务中所有的工作在提交时，即使它是分阶段执行的，也要保证安全地应用于数据库，不被其他的连接干扰。事务工作也可以在请求发生错误时轻松地自动取消。

<font color="red">那具体PDO和Mysqli的区别如下图：</font>


|         | PDO           | MySQLi  |
| ------------- |:-------------:| -----:|
| Database support      | 12 different drivers | MySQL only |
| API      | OOP      |   OOP + procedural |
| Connection | Easy      |    Easy |
| Named parameters | Yes      |    No |
| Object mapping | Yes      |    Yes |
| Prepared statements(client side) | Yes      |    No |
| Performance | Fast      |    Fast |
| Stored procedures | Yes      |    Yes |


上面说了PHP连接我们的Mysql数据库。

我们简单说一下使用命令行来操作我们的数据库。

1. 打开我们的命令行
2. 运行 `mysql -uroot -p`
3. 会提示你输入密码，当你输入密码时你就进去了。