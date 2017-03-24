---
layout: post
title:  "redis的安装和使用"
date:   2016-7-2 20:56:01 +0800
categories: redis
tag: 小记
---

* content
{:toc}

####<font color="red">windows下的安装和使用</font>

1. 下载redis程序软件：redisbin32、redisbin64
2. 不需要安装直接使用
3. 用doc进入解压过的redis目录，连接reids
redis-server.exe redis.conf?? //进入redis目录 开启redis服务命令重新开启一个cmd命令窗口开始链接redis服务
redis-cli.exe -h 192.168.12.21? //要连接的redis服务器
4. 连接redis进行操作

####<font color="red">linux下的安装和使用</font>


如果安装过程前没有安装GCC请先安装  命令：

	$ yum install gcc-c++

1. 将redis的安装软件下载到linux下/user/local/src（redis命令手册http://readthedocs.org/en/latest/）
2. tar -zxvf redis压缩包
3. 进入到解压好的文件夹后，直接make
4. 进入到src目录，将src下6个为绿色的文件和他的上一级目录中的redis.conf拷贝(cp)到你的工作目录（user/local/myredis）
5. 进入工作目录（/user/local/myredis）下
6. 执行redis.server redis.conf默认是前段启动（会占用你的控制台），修改redis.conf为后台进行（把redis.conf中的daemonize 改为yes）
7. netstat -anp \| grep 6379（过滤）

####<font color="red">简单使用</font>

![use_redis]({{ '/styles/images/use_redis.png' | prepend: site.baseurl  }})
