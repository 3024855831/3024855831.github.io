---
layout: post
title:  "面向对象"
date:   2016-10-20 20:56:01 +0800
categories: 面向对象
tag: 小记
---

* content
{:toc}

####<font color="red">面向对象（OO）</font>包括3部分内容：

1. 面向对象分析（Object Oriented Analysis,OOA）
2. 面向对象设计（Object Oriented Design,OOD）
3. 面向对象编程（Object Oriented Programming,OOP）

###类和对象:
类：<font color="red">具有相同属性和方法的事物的集合，是抽象的。</font>

对象：<font color="red">是类的实例化结果，是具体的。</font>

比如：说学生（模糊的抽象的一类），而具体的一个张三学生就是一个对象。

类和对象的关系：

蓝球运动员抽象为一个类，姚明，易建联则分别是该类的一个对象。

属性：姓名、性别、身高、体重；
行为(方法)：吃饭、接球、运球、扣篮；

歌唱家抽象为一个类，周杰伦、张杰则分别是该类的一个对象。

属性：姓名、性别；

行为(方法)：吃饭、唱歌

类和对象关系：<font color="red">类是对象的抽象，对象是类的实例化结果</font>

####<font color="red">类的组成：</font>

1. 属性（也称变量或成员变量）
2. 方法（类中的函数被称为方法或成员方法）
3. 常量  (无法更改或撤销定义)

####<font color="red">类的定义：</font>

定义方式：class 关键字
定义成员变量的格式一般为：<font color="red">变量声明符  成员变量名</font>

	class  类名
	{        
	    public  变量名；  //类属性
	    function  方法名(){
	        //函数代码
	    }
	}

####<font color="red">类的实例化：</font>

类的使用：定义类之后，如果想使用类，一般需先实例化成对象。

new 对象时：

1. 申请内存，生成对象（属性和方法的集合）
2. 如果有构造函数，则执行
3. 返回该对象的地址

例如:

	$obj =  new  类名();  	//为类实例化对象
	echo $obj->属性名; 	
	//调用输出类中定义的属性（属性名前没有$符号）。
	$obj->方法名(); 			//调用输出类中定义的方法

<font color="red">注意：除了属性和方法外，还有常量和静态成员。常量和静态可以直接通过类名访问</font>

###<font face="STCAIYUN" color='red'>面向对象的三大特性：</font>

继承：

继承是面向对象的另一个基本概念，是实现其表达能力的一个重要方面，该术语指一种关系，在这种关系中，一个雷被定义为另一个类的子类，

多态：

多态是面向对象编程的另一个强大功能，不同的对象能够共享同一个接口，因此可以实现交换，

封装：

是面向对象编程的一个基本概念，表示一个类应该具有一个公共接口和一个私有实现。

###<font face="STCAIYUN" color='red'>构造函数和析构函数：</font>

构造函数是一种特殊的方法，在第一次实例化或创建对象时使用，被命名为__construct

析构函数是构造函数的补充，被命名为__destruct

###<font face="STCAIYUN" color='red'>魔术方法：</font>

魔术方法是执行特殊的内部的PHP类函数的方法集合。

如下：

1. __construct() 
实例化对象时被调用， 
当__construct和以类名为函数名的函数同时存在时，__construct将被调用，另一个不被调用。 

2. __destruct() 
当删除一个对象或对象操作终止时被调用。 

3. __call() 
对象调用某个方法， 
若方法存在，则直接调用； 
若不存在，则会去调用__call函数。 

4. __get() 
读取一个对象的属性时， 
若属性存在，则直接返回属性值； 
若不存在，则会调用__get函数。 

5. __set() 
设置一个对象的属性时， 
若属性存在，则直接赋值； 
若不存在，则会调用__set函数。 

6. __toString() 
打印一个对象的时被调用。如echo $obj;或print $obj; 

7. __clone() 
克隆对象时被调用。如：$t=new Test();$t1=clone $t; 

8. __sleep() 
serialize之前被调用。若对象比较大，想删减一点东东再序列化，可考虑一下此函数。 

9. __wakeup() 
unserialize时被调用，做些对象的初始化工作。 

10. __isset() 
检测一个对象的属性是否存在时被调用。如：isset($c->name)。 

11. __unset() 
unset一个对象的属性时被调用。如：unset($c->name)。 

12. __set_state() 
调用var_export时，被调用。用__set_state的返回值做为var_export的返回值。 

13. __autoload() 
实例化一个对象时，如果对应的类不存在，则该方法被调用。 


<font color="red">$this 是什么意思？</font>

是正在运行的方法所属的对象，它允许当打访问属于该特定对象的其他方法和变量。

###<font face="STCAIYUN" color='red'>静态成员：</font>

静态分为两个部分：静态属性和静态方法
注意：

<font color='red'>静态方法中，只能调用静态变量，而不能调用普通变量，但普通方法中可以调用静态变量。</font>

####静态属性

定义静态属性：使用关键字static修饰的属性称之为静态属性。

####静态方法

定义静态方法：使用static关键字修饰的方法叫做静态方法。

例子：

	class Teacher{
		static public $username="张三";   //定义静态属性
		static function show(){            //定义静态方法
			echo "姓名是:".self::$username;
		}
	}
	//调用类内部的静态属性/静态方法  关键字::静态成员名字
	ECHO Teacher::$username;
	Teacher::show();

###<font face="STCAIYUN" color='red'>self与$this的区别：</font>

1. self ：代表本类，自身（不要理解为本类的对象），$this代表对象
2. self访问类内部的常量和静态成员，$this访问对象的属性和普通方法
3. self必须配合范围解析操作符（::）才能生效，$this代表对象，对象本来就是一种数据类型，所以$this可以单独被打印。
4. 能用$this的地方，一定可以使用self，但是能使用self的地方不一定可以使用$this
5. 非静态的属性和方法均用对象（$this）访问，静态的方法和属性或常量均用类(self)来访问