---
layout: post
title:  "Mysql事务处理"
date:   2014-12-18 20:56:01 +0800
categories: mysql
tag: 小记
---

* content
{:toc}


1、什么是事务？

   事务是作为一个不可分割的逻辑单元而被执行的一组sql语句，要么同时执行成功要么撤销。

2、事务的四个特性？（ACID）

1. 原子性：构成一个事务的所有语句应该是一个独立的逻辑单元，要么全部执行成功，要么一个都不成功。你不能只执行它们当中的一部分。
2. 稳定性(一致性):  数据库在事务开始执行之前和事务执行完毕之后都必须是稳定的。换句话说，事务不应该把你的数据库弄得一团糟。
3. 隔离性(孤立性):  事务不应该相互影响。
4. 可靠性(持久性): 如果事务执行成功，它的影响将被永久性地记录到数据里。
    
3、使用事务的前提条件是什么呢？ 

表的存储引擎必须是innodb

4、使用事务

我们先来创建一个银行的转账表,字段为用户id、用户名、钱，这里注意下我们使用的是innodb的存储引擎。

	CREATE TABLE `brank`.`bank` (
	`userid` INT NOT NULL AUTO_INCREMENT ,
	`name` VARCHAR( 20 ) NOT NULL ,
	`money` INT NOT NULL ,
	PRIMARY KEY ( `userid` ) 
	) ENGINE = InnoDB;

然后插入两条测试数据:

	INSERT INTO `brank`.`bank` (
	`userid` ,
	`name` ,
	`money` 
	)
	VALUES (
	NULL , '张三', '1000'
	), (
	NULL , '李四', '1'
	);
	
查看结果:

+--------+------+-------+
| userid | name | money |
+--------+------+-------+
|      1 | 张三 |  1000 |
|      2 | 李四 |     1 |
+--------+------+-------+
2 rows in set (0.00 sec)
    

现在我们来实现这个转账的过程,根据上面的分析我们知道这需要两条sql语句来实现。假设我们要实现张三转800元给李四？

  第一:我们要修改张三的记录将money字段的值减去800

  第二:我们要修改李四的记录将 money字段的值增加800
  
在默认的情况下,mysql从自动提交模式运行，这种模式会在每条语句执行完毕后把它作出的修改立刻提交给数据库并使之永久化。事实上，这相当于把每一条语句都隐含地当做一个事务来执行。如果你想明确地执行事务，需要禁用自动提交模式并告诉mysql你想让它在何时提交或回滚有关的修改。
 	
执行事务的常用办法是发出一条start transaction或begin语句挂起自动提交模式，然后执行构成本次事务的各条语句，最后用一条commit语句结束事务并把它们作出的修改永久性的记入数据库。万一在事务过程中发生错误，用一条rollback语句撤销事务并把数据库恢复到事务开始之前的状态。

1) 现在我们来开始事务:

Mysql>Begin;
      Query OK, 0 rows affected (0.00 sec)

执行第一条修改句

Mysql>update bank set money = money -800 where name = ‘张三’;
Query OK, 1 row affected (0.05 sec)
Rows matched: 1  Changed: 1  Warnings: 0

执行第二条修改语句

Mysql>update bank et money = money + 800 where name = ‘李四’;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that
corresponds to your MySQL server version for the right syntax to use near 'money
 = money + 800 where name = '李四'' at line 1

这个时候语句出错了，想想我们应该怎么办?那我们就让事务回滚一下

2) 事务回滚:

Mysql > rollback;
Query OK, 0 rows affected (0.05 sec)
Mysql > select * from bank;

+--------+------+-------+
| userid | name | money |
+--------+------+-------+
|      1 | 张三 |  1000 |
|      2 | 李四 |     1 |
+--------+------+-------+
2 rows in set (0.00 sec)

看到效时了吧，和执行事务之前的数据状态一样。这就是使用事务的好处

3) 自动提交模式（mysql默认的提交模式）

Set autocommit = 1; 

非自动提交模式

Set autocommit = 0;