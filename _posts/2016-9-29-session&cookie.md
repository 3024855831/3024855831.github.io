---
layout: post
title:  "session & cookie"
date:   2016-9-29 13:56:01 +0800
categories: 存储
tag: 小记
---

* content
{:toc}

###<font color="red">cookie技术：</font>是一种服务器将数据保存到浏览器，然后浏览器在下次访问该网站的时候，会自动将服务器保存的数据携带给服务器的技术。

<font color="red">Cookie的类型</font>

Cookie总时由用户客户端进行保存的（一般是浏览器），按其存储位置可分为：内存式Cookie和硬盘式Cookie。

1. 内存式Cookie存储在内存中，浏览器关闭后就会消失，由于其存储时间较短，因此也被称为非持久Cookie或会话Cookie。

2. 硬盘式Cookie保存在硬盘中，其不会随浏览器的关闭而消失，除非用户手工清理或到了过期时间。由于硬盘式Cookie存储时间是长期的，因此也被称为持久Cookie。

下面是一个实现Cookie机制的，简单的HTTP请求过程：

![cookie]({{ '/styles/images/cookie_one.png' | prepend: site.baseurl  }})

<font face="STCAIYUN" color="red">在php中如何操作cookie:</font>

存：

	$_COOKIE['id'] = '1';

取：
	
	$id = $_COOKIE['id'];

###<font color='red'>Session:</font>
在计算机中，尤其是在网络应用中，称为“会话控制”。Session 对象存储特定用户会话所需的属性及配置信息。

利用 Cookie 管理 Session:

![session]({{ '/styles/images/session_one.jpg' | prepend: site.baseurl  }})

上图所述：

1. 客户端把用户 ID 和密码等登录信息放入报文的实体部分，通常是以 POST 方法把请求发送给服务器。

2. 服务器会发放用以识别用户的 Session ID。通过验证从客户端发送过来的登录信息进行身份验证，然后把用户的认证状态与 Session ID 绑定后记录在服务器端。向客户端返回响应时，会在首部字段 Set-Cookie 内写入 Session ID。

3. 客户端接收到从服务器端发来的 Session ID 后，会将其作为 Cookie 保存在本地。下次向服务器发送请求时，浏览器会自动发送 Cookie，所以 Session ID 也随之发送到服务器。服务器端可通过验证接收到的 Session ID 识别用户和其认证状态。

<font face="STCAIYUN" color="red">在php中如何操作session：</font>
	
首先要开启session
	
	session_start();

存：

	$_SESSION['id'] = '1';

取：

	$id = $_SESSION['id'];