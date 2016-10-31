---
layout: post
title:  "自己动手搭建MVC之四"
date:   2016-2-10 10:01:01 +0800
categories: 框架
tag: 小记
---

* content
{:toc}

我们今天讲的在我们搭建的框架使用composer。

<font face="STCAIYUN" color='red'>Composer的使用</font>

1. 安装composer，在composer官网上下载就行了，具体我们这里就先跳过。
 
2. 在我们框架的根目录中新建一个composer.json的文件来加载我们的composer的使用。
 
3. 在我们的composer.json中写入


		{
		"name": "XING PHP",//框架的名称

		"description": "PHP Framework",//简单的描述

		"type": "Framework",//类型

		"keywords":[//关键字

		"PHP","PHP Framework"

		],

		"require":{

			"php":">=5.3.0",//PHP的版本

			"filp/whoops":"*",//我们要下载的第三方类

		}

		}


我们这里以filp/whoops（错误展示类）为例。
 
4. 使用命令行进入我们的框架的根目录，composer install就可以。
 
5. 引入第三方的类库，我们通常在入口文件中来引入我们的第三方类库。如上面的whoops这个类，我们就可以直接引入

		include "vendor/autoload.php";

		$whoops = new \Whoops\Run;

		$whoops->pushHandler(new \Whoops\Handler\PrettyPageHandler);

		$whoops->register();

就可以使用了。
 
<font face="STCAIYUN" color='red'>数据库操作第三方类</font>

另外我们也可以利用composer来下载一个数据库操作的第三方类库。
我们拿medoo这个数据库操作的第三方类为例。

1. 我们在composer.json中require加入"catfan/medoo":"*"。来下载我们需要的类，然后进入框架的根目录中，composer update就下载完成了。
 
2. 我们在model的基类直接继承我们medoo这类就行了，链接我们的数据库就可以使用，具体使用方法见medoo手册。