---
layout: post
title:  "JavaScript"
date:   2016-10-10 12:56:01 +0800
categories: JavaScript
tag: 小记
---

* content
{:toc}

####<font color="red">javascript：</font>JavaScript是直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。它的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。

特点：JavaScript是一种基于对象和事件驱动并具有安全性能的脚本语言

作用：制作网页特效、实现表单验证、增加浏览器与用户交互的动态效果

<font color="red">javascript的数据类型</font>

1. 数值型：例如 3  5  1.2  3.4

2. 布尔：两个值真或假，如true或false 
3. 字符串：例如: ‘I am a jelly doughnut’由一个或多个字符组成,
 用单引号或双引号引起来的一系列的字符(也可以称之为一个			  字符串对象）
4. 空值：用关键字NULL表示．如果变量声明但是没有赋值就是这个类型
5. 未定义：用关键字undefined表示，如果变量未声明则就是未定义类型
6. 数组：用new Array()声明的就是数据(也可以称之为一个数组对象)
7. 对象：{}使用一对花括号声明的就是一个对象

1. 内存式Cookie存储在内存中，浏览器关闭后就会消失，由于其存储时间较短，因此也被称为非持久Cookie或会话Cookie。

2. 硬盘式Cookie保存在硬盘中，其不会随浏览器的关闭而消失，除非用户手工清理或到了过期时间。由于硬盘式Cookie存储时间是长期的，因此也被称为持久Cookie。

下面是javascript的运算符：

![arithmetic]({{ '/styles/images/arithmetic.png' | prepend: site.baseurl  }})

###<font face="STCAIYUN" color="red">JavaScript中的事件</font>

鼠标事件（onclick、onmouseover、onmouseout、onmousemove）

 Onclick：鼠标单击事件，当鼠标单击时此事件触发
  例如：单击鼠标按钮更改页面的背景颜色

        <meta charset=utf-8>
		<input type='button' value="更改背景颜色" onclick='fun()'>
		<script>
		function fun(){
			document.bgColor='red'
		}
		</script>

 Onmouseover：鼠标移上事件，当鼠标移上某个元素时此事件触发
 Onmouseout：鼠标移出事件，当鼠标移出某个元素时此事件触发
 例如：鼠标移到p标签上的时候更改文字内容

	<meta charset=utf-8>
	<a id='content' onmouseover='fun()' href='' onmouseout='fun2()'>请移动上来</a>
	<script>
	function fun(){
		document.getElementById("content").innerHTML='我被改变了'
	}
	function fun2(){
		document.getElementById("content").innerHTML='请移动上来'
	}
	</script>

 Onmousemove：鼠标移动事件，当鼠标在某个元素上移动的时候此事件触发
 例如：当鼠标经过图片的时候给出提示

	<meta charset=utf-8>
	<img src='a.jpg' onmousemove='fun()'> 
	<script>
	function fun(){
		alert("鼠标经过我啦！")
	}
	</script>

键盘事件（onkeydown、onkeyup、onkeypress）

Onkeydown：键盘按下事件，当按下键盘的时候此事件触发
  例如：按下键盘时给出提示

	<meta charset=utf-8>
	<input type='text' id='username' onkeydown='fun()' > 
	<script>
	function fun(){
		alert("键盘按下了!")
	}
	</script>

  Onkeyup：键盘抬起事件，当抬起键盘的时候此事件触发
  例如：抬起键盘时给出提示

	<meta charset=utf-8>
	<input type='text' id='username' onkeyup='fun()' > 
	<script>
	function fun(){
		alert("键盘抬起了!")
	}
	</script>

页面事件（onload、onunload）

Onload：页面加载事件，当打开这个页面的时候此事件触发

  Onunload：页面卸载事件，当关闭页面的时候此事件触发
  例如：加载文档的时候提示欢迎光临，关闭时提示谢谢

	<meta charset=utf-8" />
	<script type="text/javascript">
		function aa(){
			alert("欢迎xxx光临");
		}
		function bb(){
			alert("谢谢huigu");
		}	
	</script>
	<body onload="aa()" onunload="bb()"></body>

表单事件（onblur、onsubmit、onchange）

Onblur：失去焦点事件，当光标离开文本框时此事件触发
  例如：失去焦点的时候验证用户名和密码非空

	  <script>
	function check_name(){
		var name=document.getElementById("name").value;
		if(name==""){
			document.getElementById("s_name").innerHTML="<font color='red'>用户名不能为空</font>";
			return false;		
		}else{
			document.getElementById("s_name").innerHTML="";
			return true;
		}
	}
	function check_pwd(){
		var name=document.getElementById("pwd").value;
		if(name==""){
			document.getElementById("s_pwd").innerHTML="<font color='red'>密码不能为空</font>";
			return false;
		}else{
			document.getElementById("s_pwd").innerHTML="";
			return true;
		}
	}
	</script>
	<form action='第一天检测.html' >
	用户名：
	<input type='text' id='name' onblur='check_name()'>
	<span id='s_name'></span><p>
	密码：
	<input type='text' id='pwd' onblur='check_pwd()'>
	<span id='s_pwd'></span><p>
	<input type='submit' value='登录' >
	</form>

Onsubmit：表单提交事件，当点击提交按钮的时候此事件触发
    例如：点击提交按钮的时候判断用户名和密码框不为空才能提交

	<form action='第一天检测.html' onsubmit='return sub()'>
	用户名：
	<input type='text' id='name' onblur='check_name()'>
	<span id='s_name'></span><p>
	密码：
	<input type='text' id='pwd' onblur='check_pwd()'>
	<span id='s_pwd'></span><p>
	<input type='submit' value='登录' >
	</form>
	<script>
	function check_name(){
		var name=document.getElementById("name").value;
		if(name==""){
			document.getElementById("s_name").innerHTML="<font color='red'>用户名不能为空</font>";
			return false;	
		}else{
			document.getElementById("s_name").innerHTML="";
			return true;
		}
	}
	function check_pwd(){
		var name=document.getElementById("pwd").value;
		if(name==""){
			document.getElementById("s_pwd").innerHTML="<font color='red'>密码不能为空</font>";
			return false;	
		}else{
			document.getElementById("s_pwd").innerHTML="";
			return true;
		}
	}
	//表单提交验证的函数
	function sub(){
		//当用户名验证和密码验证都合法的时候才进行表单提交
		if(check_name()&&check_pwd()){
			return true;
		}else{
			return false;
		}
	}
	</script>

Onchange：内容改变事件，当改变内容时此事件触发
例如：改变下拉框的值来改变背景颜色

      <meta charset=utf-8>
	请选择背景颜色：<select id='data' onchange='fun()'>
		<option value='red'>红色</a>
		<option value='yellow'>黄色</a>
		<option value='blue'>蓝色</a>
	</select>
	<script>
	function fun(){
		var i=document.getElementById("data").value;
		document.bgColor=i;
	}
	</script>

DOM编程的基本找对象方法:

1. 通过id找对象：document.getElementById(“元素id”)
2. 通过name找对象：document.getElementsByName(“元素name”)
3. 通过标签找对象：document.getElementsByTageName(“标签名”)
4. 通过forms找对象：document.forms[0]找到html文档中第一个表单，[]里

history对象的方法:

 1. History.go(-1)：后退
 2. History.go(0)：刷新
 3. History.go(1)：前进
 4. History.back()：后退
 5. History.forward()：前进


##<font face="STCAIYUN" color="red">正则表达式</font>

模式匹配符：

  \：转义字符  例如：\b转义了b

  ^：正则表达式开始符号

  $：正则表达式结束符号

  *：匹配前面的字符出现0次或者n次

  +：匹配前面的字符出现1次或者n次

  ?：匹配前面的字符出现0次或者1次

  .：匹配除了换行符以外的所有单个字符

  |：或者的意思，例如x|y  匹配x或者y

  {n}：匹配前面的n个字符

  {n,m}：匹配至少n个最多m个前面字符

  [xyz]：匹配中括号里的任意一个字符

  [^xyz]：匹配除了中括号里的任意一个字符等价于[0-9]

  \w：匹配任意一个数字或字母或下划线 等价于[A-Za-z0-9_]

  \d：匹配任意一个0--9之间的数字

  模式修正符：

  i：忽略大小写

###通常用到的正则表达式

	//用户名由6-18位的字母数字下划线组成，不能由数字开头
	var r_name=/^[a-z]\w{5,17}$/i
	//密码长度不能少于六位
	var r_pwd=/^\w{6,}$/
	//所有的通用邮箱地址
	var r_eamil=/^\w+@\w+(\.)\w+$/
	//匹配一个QQ邮箱地址
	//861745122@qq.com 
	var r_qq_email=/^\d{5,}@qq(\.)com$/
	//匹配一个163的邮箱地址
	var r_163_email=/^\w+@163(\.)com$/
	//匹配一个后缀名可能是.com|.net|.cn|.edu
	var email=/^\w+@\w+(\.)com|net|cn|edu$/
	//要求输入有效的年龄段
	var r_age=/^\d{1,2}$/
	//if(age>=18&&age<=100)
	//验证手机号:11位  13 15 18开头
	var r_tel=/^1[3,5,8]\d{9}$/
	//验证身份证号  18位或者17位加一个X
	var r_s=/^\d{18}|\d{17}x$/i
	//验证中文
	var reg=/^[\u4e00-\u9fa5]{2,17}$/