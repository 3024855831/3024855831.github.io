---
layout: post
title:  "微信支付"
date:   2016-9-10 13:56:01 +0800
categories: wechat
tag: 小记
---

* content
{:toc}

###<font color="red">微信支付：</font>


<font color="red">支付模式：</font>

1、刷卡支付
刷卡支付是用户展示微信钱包内的“刷卡条码/二维码”给商户系统扫描后直接完成支付的模式。主要应用线下面对面收银的场景。

2、扫码支付
扫码支付是商户系统按微信支付协议生成支付二维码，用户再用微信“扫一扫”完成支付的模式。该模式适用于PC网站支付、实体店单品或订单支付、媒体广告支付等场景。

3、公众号支付
公众号支付是用户在微信中打开商户的H5页面，商户在H5页面通过调用微信支付提供的JSAPI接口调起微信支付模块完成支付。应用场景有：
	用户在微信公众账号内进入商家公众号，打开某个主页面，完成支付
	用户的好友在朋友圈、聊天窗口等分享商家页面连接，用户点击链接打开商家页面，完成支付
	将商户页面转换成二维码，用户扫描二维码后在微信浏览器中打开页面后完成支付

4、APP支付
APP支付又称移动端支付，是商户通过在移动端应用APP中集成开放SDK调起微信支付模块完成支付的模式。

<font color="red">关于安全：</font>

签名算法------（签名校验工具）
签名生成的通用步骤如下：

第一步，设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…）拼接成字符串stringA。

特别注意以下重要规则：

◆ 参数名ASCII码从小到大排序（字典序）；

◆ 如果参数的值为空不参与签名；

◆ 参数名区分大小写；

◆ 验证调用返回或微信主动通知签名时，传送的sign参数不参与签名，将生成的签名与该sign值作校验。

◆ 微信接口可能增加字段，验证签名时必须支持增加的扩展字段

第二步，在stringA最后拼接上key得到stringSignTemp字符串，并对stringSignTemp进行MD5运算，再将得到的字符串所有字符转换为大写，得到sign值signValue。
key设置路径：微信商户平台(pay.weixin.qq.com)-->账户设置-->API安全-->密钥设置
举例：
假设传送的参数如下：

	appid：	wxd930ea5d5a258f4f
	mch_id：	10000100
	device_info：	1000
	body：	test
	nonce_str：	ibuaiVcKdpRxkhJA

第一步：对参数按照key=value的格式，并按照参数名ASCII字典序排序如下：

	stringA="appid=wxd930ea5d5a258f4f&body=test&device_info=1000&mch_id=10000100&nonce_str=ibuaiVcKdpRxkhJA";

第二步：拼接API密钥：

	stringSignTemp="stringA&key=192006250b4c09247ec02edce69f6a2d"
	sign=MD5(stringSignTemp).toUpperCase()="9A0A8659F005D6984697E2CA0A9CF3B7"

最终得到最终发送的数据：

	<xml>
	<appid>wxd930ea5d5a258f4f</appid>
	<mch_id>10000100</mch_id>
	<device_info>1000<device_info>
	<body>test</body>
	<nonce_str>ibuaiVcKdpRxkhJA</nonce_str>
	<sign>9A0A8659F005D6984697E2CA0A9CF3B7</sign>
	<xml>

2、生成随机数算法
微信支付API接口协议中包含字段nonce_str，主要保证签名不可预测。我们推荐生成随机数算法如下：调用随机数函数生成，将得到的值转换为字符串。

<font color="red">OpenID：</font>

微信公众平台：

在关注者与公众号产生消息交互后，公众号可获得关注者的OpenID（加密后的微信号，每个用户对每个公众号的OpenID是唯一的。对于不同公众号，同一用户的openid不同）。

公众号可根据以下接口来获取用户的openid，如需获取用户的昵称、头像、性别、所在城市、语言和关注时间，则需要用户授权。

参考信息：

	http://mp.weixin.qq.com/wiki/17/c0f37d5704f0b64713d5d2c37b468d75.html

开发者如果需要将同一个用户在不同公众号下的openid统一为一个id来记录，可以参考以下接口：

参考信息：

	http://mp.weixin.qq.com/wiki/14/bb5031008f1494a59c6f71fa0f319c66.html
 
微信开放平台：
移动应用获取用户openid可使用以下接口：

	https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419317851&token=&lang=zh_CN

网站应用获取用户openid可使用以下接口：

	https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419316505&token=&lang=zh_CN

<font color="red">SDK下载地址：</font>

[https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=11_1](https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=11_1) 

<font color="red">公众号支付开发步骤：</font>

1、设置测试目录
在微信公众平台设置，栏目见图7.7。支付测试状态下，设置测试目录，测试人的微信号添加到白名单，发起支付的页面目录必须与设置的精确匹配。并将支付链接发到对应的公众号会话窗口中才能正常发起支付测试。注意正式目录一定不能与测试目录设置成一样，否则支付会出错。

微信内网页支付设置栏目入口

![wechat_pay_1]({{ '/styles/images/wechat_pay_1.png' | prepend: site.baseurl  }})


2、设置正式支付目录
根据图中栏目顺序进入修改栏目，勾选JSAPI网页支付开通该权限，并配置好支付授权目录，该目录必须是发起支付的页面的精确目录，子目录下无法正常调用支付。具体界面如图所示：

![wechat_pay_2]({{ '/styles/images/wechat_pay_2.png' | prepend: site.baseurl  }})


