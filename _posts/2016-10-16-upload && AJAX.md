---
layout: post
title:  "upload & 分页 & AJAX"
date:   2016-10-16 20:56:01 +0800
categories: AJAX
tag: 小记
---

* content
{:toc}

####<font color="red">上传的原理：</font>文件由客户端通过post方式移动到服务器端临时文件夹里，再从临			 时文件夹里上传到服务器端指定的目录里的过程成为文件上传。

实现步骤：

1. 首先在表单页面将提交方式声明成post没加上文件上传头信息如下图

![headinfo]({{ '/styles/images/headinfo.png' | prepend: site.baseurl  }})

在action指定的文件里用$_FILES数组来接收上传信息，设定文件上传的目录，通过文件上传移动函数move_uploaded_file()移动文件到服务器端的文件夹里。

其中$_FILES数组中包含如下信息：

![headinfo]({{ '/styles/images/imginfo.png' | prepend: site.baseurl  }})

<font color='red'>文件上传相关函数:</font>

Move_uploaded_file()：将上传文件移动到指定的位置，如果成功则返回true，否则返回false

####<font color='red'>分页的原理:</font>

####将数据从数据库中按照limit关键字进行分段查询，从而减轻数

###分页步骤:

1. 查询出参与分页数据的总记录数
2. 设定每页显示多少条数据
3. 计算出总页数：ceil（总记录数/每页显示的条数）
4. 获取当前页：$page=$_GET[‘page’]?$_GET[‘page’]:1;
5. 计算偏移量：(当前页-1)*每页显示的条数
6. 查询数据：select * from 表名 limit 偏移量,每页显示的条数
7. 输出上一页、下一页、首页、尾页的超链接

###<font color="red">ajax技术：</font>ajax是一种技术，它是由div+css javascript和xml技术组成。作用：异步存取，局部刷新，能实现无页面刷新的效果

####<font color="red">ajax的优缺点：</font>

Ajax优点：可以减轻服务器处理数据的压力，实现无页面刷新，增强用户体验。

Ajax缺点：不利于SEO（搜索引擎）优化

Ajax应用场景：在页面显示大量数据，实时更新的网站上，实现局部刷新

###<font color="red">ajax的运行原理：</font>

   客户端浏览器通过ajax引擎发送请求，服务器接收请求后通过php访问数据库处理数据，处理完的数据通过ajax引擎响应给客户端，客户端通过js把数据放到需要的地方。

	    		 客户端
                请求  |  |  响应
                   ajax引擎
                      |  |
                 Web服务器apache
                  访问|  |返回
                     数据库

##<font face="STCAIYUN" color="red">ajax的核心代码</font>

a.ajax对象：var ajax= new XMLHttpRequest();

b.ajax属性
   1)readyState：ajax对象的准备状态，状态从0----4发生变化

　　	0：请求未初始化
　　	1：服务器连接已建立
　　	2：请求已接收
　　	3：请求处理中
　　	4：请求已完成且响应已就绪

  2)responseText：响应文本 

  3)status状态： 值为200表示处理成功 值为404表示没有找到处理文件

  c.ajax事件 onreadystatechange

  d.ajax方法

  1)ajax.open()：与服务器建立连接（get（提交方式 url（地址） 
  true（异步））

  2)ajax.send()：处理请求

  例如：

Get方式请求：

	//1.创建ajax对象
	var ajax= new XMLHttpRequest();
	//2.ajax事件
	ajax.onreadystatechange = function(){
	if(ajax.readyState ==4) {
	//处理语句
	} 
	}
	//3.与服务器建立连接
	ajax.open('get',url,false);
	//4. 服务器处理请求
	ajax.send(null);

Post方式请求：

	//创建ajax对象
	var ajax= new XMLHttpRequest();
	//ajax事件
	ajax.onreadystatechange = function(){
	if(ajax.readyState ==4)   {
	} 
	}
	//与服务器建立连接
	ajax.open('post',url,false);
	ajax.setRequestHeader('Content-Type','application/x-www-form-urlencoded'); 
	//处理请求
	ajax.send('name='+name+”&id=”+id);

js实现全选全不选:

	<meta charset=utf-8>
	全选/全不选<input type="checkbox" id="quanxuan"  onclick="checkAll()"><p>
	<input type="checkbox" name="data[]">蔬菜<p>
	<input type="checkbox" name="data[]">酒水<p>
	<input type="checkbox" name="data[]">水果<p>
	<input type="checkbox" name="data[]">饮料<p>
	<input type="checkbox" name="data[]">香烟<p>
	<input type="checkbox" name="data[]">辣条<p>
	<input type="checkbox" name="data[]">烤鸭<p>
	<script>
	function checkAll(){
		var obj=document.getElementById("quanxuan");
	    //找到所有的复选款对象
		var data=document.getElementsByName("data[]");
		//先判断全选框是否选中
		if(obj.checked==true){
			for(i in data){
				if(data[i].checked==false){
					data[i].checked=true
				}
			}
		}else{
			for(i in data){
				if(data[i].checked==true){
					data[i].checked=false
				}
			}
		}
	}
	</script>
