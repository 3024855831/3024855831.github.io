---
layout: post
title:  "自己动手搭建MVC之五"
date:   2016-2-11 12:01:01 +0800
categories: 框架
tag: 小记
---

* content
{:toc}

我们今天要讲的是一个模板引擎的使用，关于模板引擎我们也是使用composer来进行下载的。

<font face="STCAIYUN" color='red'>twig模板引擎</font>

1. 在composer.json中require加入"twig/twig":"*"。来下载我们需要的类，然后进入框架的根目录中，composer update就下载完成了。
 
2. 我们既然有了模板引擎了，我们就不需要来自己写一些东西，在我们之二的display方法中直接引入下面这段直接使用：

		\Twig_Autoloader::register();
		$loader = new \Twig_Loader_Filesystem(APP.'/view');
		$twig = new \Twig_Environment($loader, array(
		'cache' => '/path/to/compilation_cache',
		'debug' => DEBUG
		));
		$template = $twig->loadTemplate('index.html');
		$template->display($this->assign?$this->assign:array());
		
这样我们就可以使用twig这个模板引擎了，具体使用方法见twig手册。
 
到这里呢我们的框架就已经基本成型了，下面来试试我们自己搭建的框架吧！