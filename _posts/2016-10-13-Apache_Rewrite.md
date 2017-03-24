---
layout: post
title:  "实用的Apache Rewrite重写规则"
date:   2016-10-13 20:56:01 +0800
categories: http
tag: 小记
---

* content
{:toc}

1．去掉域名中的www标记
代码如下:

	RewriteCond %{HTTP_HOST} !^jb51\.net$ [NC]
	RewriteRule .? http://jb51.net%{REQUEST_URI} [R=301,L]

2．去掉www标记，但是保存子域名
代码如下:

	RewriteCond %{HTTP_HOST} ^www\.(([a-z0-9_]+\.)?jb51\.net)$ [NC]
	RewriteRule .? http://%1%{REQUEST_URI} [R=301,L]

这里，当匹配到1%变量以后，子域名才会在%2（内部原子）中抓取到，而我们需要的正是这个%1变量。
3．给子域名加www标记
代码如下:

	RewriteCond %{HTTP_HOST} ^([a-z.]+)?jb51\.net$ [NC]
	RewriteCond %{HTTP_HOST} !^www\. [NC]
	RewriteRule .? http://www.%1jb51.net%{REQUEST_URI} [R=301,L]

这个规则抓取二级域名的%1变量，如果不是以www开始，那么就加www，以前的域名以及{REQUEST_URI}会跟在其后。

4．防止图片盗链
一些站长不择手段的将你的图片盗链在他们网站上，耗费你的带宽。你可以加一下代码阻止这种行为。
代码如下:

	RewriteCond %{HTTP_REFERER} !^$
	RewriteCond %{HTTP_REFERER} !^http://(www\.)?jb51\.net/ [NC]
	RewriteRule \.(gif|jpg|png)$ – [F]

如果{HTTP_REFERER}值不为空，或者不是来自你自己的域名，这个规则用[F]FLAG阻止以gif|jpg|png 结尾的URL
如果对这种盗链你是坚决鄙视的，你还可以改变图片，让访问盗链网站的用户知道该网站正在盗用你的图片。
代码如下:

	RewriteCond %{HTTP_REFERER} !^$
	RewriteCond %{HTTP_REFERER} !^http://(www\.)?jb51\.net/.*$ [NC]
	RewriteRule \.(gif|jpg|png)$ 你的图片地址 [R=301,L]

除了阻止图片盗链链接，以上规则将其盗链的图片全部替换成了你设置的图片。
你还可以阻止特定域名盗链你的图片：
代码如下:

	RewriteCond %{HTTP_REFERER} !^http://(www\.)?leech_site\.net/ [NC]
	RewriteRule \.(gif|jpg|png)$ – [F,L]

这个规则将阻止域名黑名单上所有的图片链接请求。
当然以上这些规则都是以{HTTP_REFERER}获取域名为基础的，如果你想改用成IP地址，用{REMOTE_ADDR}就可以了。
5．如果文件不存在重定向到404页面
如果你的主机没有提供404页面重定向服务，那么我们自己创建。
代码如下:

	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteRule .? /404.php [L]

这里-f匹配的是存在的文件名，-d匹配的存在的路径名。这段代码在进行404重定向之前，会判断你的文件名以及路径名是否存在。你还可以在404页面上加一个?url=$1参数：
代码如下:

	RewriteRule ^/?(.*)$ /404.php?url=$1 [L]

这样，你的404页面就可以做一些其他的事情，例如默认信心，发一个邮件提醒，加一个搜索，等等。

6．重命名目录
如果你想在网站上重命名目录，试试这个：
代码如下:

	RewriteRule ^/?old_directory/([a-z/.]+)$ new_directory/$1 [R=301,L]

在规则里我添加了一个“.”（注意不是代表得所有字符，前面有转义符）来匹配文件的后缀名。

7．将.html后缀名转换成.php
前提是.html文件能继续访问的情况下，更新你的网站链接。
代码如下:

	RewriteRule ^/?([a-z/]+)\.html$ $1.php [L]

这不是一个网页重定向，所以访问者是不可见的。让他作为一个永久重定向（可见的），将FLAG修改[R=301,L]。

8．创建无文件后缀名链接
如果你想使你的PHP网站的链接更加简洁易记－或者隐藏文件的后缀名，试试这个:
代码如下:

	RewriteRule ^/?([a-z]+)$ $1.php [L]

如果网站混有PHP以及HTML文件，你可以用RewriteCond先判断该后缀的文件是否存在，然后进行替换：
代码如下:

	RewriteCond %{REQUEST_FILENAME}.php -f
	RewriteRule ^/?([a-zA-Z0-9]+)$ $1.php [L]
	RewriteCond %{REQUEST_FILENAME}.html -f
	RewriteRule ^/?([a-zA-Z0-9]+)$ $1.html [L]

如果文件是以.php为后缀，这条规则将被执行。

9．检查查询变量里的特定参数
如果在URL里面有一个特殊的参数，你可用RewriteCond鉴别其是否存在：
代码如下:

	RewriteCond %{QUERY_STRING} !uniquekey=
	RewriteRule ^/?script_that_requires_uniquekey\.php$ other_script.php [QSA,L]

以上规则将检查{QUERY_STRING}里面的uniquekey参数是否存在，如果{REQUEST_URI}值为script_that_requires_uniquekey，将会定向到新的URL。

10．删除查询变量
Apache的mod_rewrite模块会自动辨识查询变量，除非你做了以下改动：
a).分配一个新的查询参数（你可以用[QSA,L]FLAG保存最初的查询变量）
b).在文件名后面加一个“?”（比如index.php?）。符号“?”不会在浏览器的地址栏里显示。

11．用新的格式展示当前URI
如果这就是我们当前正在运行的URLs：/index.php?id=nnnn。我们非常希望将其更改成/nnnn并且让搜索引擎以新格式展现。首先，我们为了让搜索引擎更新成新的，得将旧的URLs重定向到新的格式，但是，我们还得保证以前的index.php照样能够运行。是不是被我搞迷糊了？
实现以上功能，诀窍就在于在查询变量中加了一个访问者看不到的标记符“marker”。我们只将查询变量中没有出现“marker”标记的链接进行重定向，然后将原有的链接替换成新的格式，并且通过[QSA]FLAG在已有的参数加一个“marker”标记。以下为实现的方式：
代码如下:

	RewriteCond %{QUERY_STRING} !marker
	RewriteCond %{QUERY_STRING} id=([-a-zA-Z0-9_+]+)
	RewriteRule ^/?index\.php$ %1? [R=301,L]
	RewriteRule ^/?([-a-zA-Z0-9_+]+)$ index.php?marker &id=$1 [L]

这里，原先的URL：http://www.jb51.net/index.php?id=nnnn,不包含marker，所以被第一个规则永久重定向到http://www.jb51.net/nnnn，第二个规则将http://www.jb51.net/nnnn反定向到http://www.jb51.net/index.php?marker&id=nnnn，并且加了marker以及id=nnnn两个变量，最后mod_rewrite就开始进行处理过程。
第二次匹配，marker被匹配，所以忽略第一条规则，这里有一个“.”字符会出现在http://www.jb51.net/index.php?marker&id=nnnn中，所以第二条规则也会被忽略，这样我们就完成了。
注意，这个解决方案要求Apache的一些扩展功能，所以如果你的网站放于在共享主机中会遇到很多障碍。

12．保证安全服务启用
Apache可以用两种方法辨别你是否开启了安全服务，分别引用{HTTPS}和{SERVER_PORT}变量：
代码如下:

	RewriteCond %{REQUEST_URI} ^secure_page\.php$
	RewriteCond %{HTTPS} !on
	RewriteRule ^/?(secure_page\.php)$ https://www.jb51.net/$1 [R=301,L]

以上规则测试{REQUEST_URI}值是否等于我们的安全页代码，并且{HTTPS}不等于on。如果这两个条件同时满足，请求将被重定向到安全服务URI.另外你可用{SERVER_PORT}做同样的测试，443是常用的安全服务端口
代码如下:

	RewriteCond %{REQUEST_URI} ^secure_page\.php$
	RewriteCond %{SERVER_PORT} !^443$
	RewriteRule ^/?(secure_page\.php)$ https://www.jb51.net/$1 [R=301,L]

13．在特定的页面上强制执行安全服务
遇到同一个服务器根目录下分别有一个安全服务域名和一个非安全服务域名，所以你就需要用RewriteCond 判断安全服务端口是否占用，并且只将以下列表的页面要求为安全服务：
代码如下:

	RewriteCond %{SERVER_PORT} !^443$
	RewriteRule ^/?(page1|page2|page3|page4|page5)$ https://www.jb51.net/%1[R=301,L]

以下是怎样将没有设置成安全服务的页面返回到80端口：
代码如下:

	RewriteCond %{ SERVER_PORT } ^443$
	RewriteRule !^/?(page6|page7|page8|page9)$http://www.jb51.net%{REQUEST_URI} [R=301,L]

其实Rewrite里运用最多的还应该是正则表达式，如果了解点儿正则的话，写起这个规则还是比较简单的。