---
layout: post
title: "云服务器代理科学上网"
date: 2018.10.12 11:02
categories: software
tag: software
---
* content
{:toc}

上回说到用22端口做转发实现代理上网，这回用真的服务器端口做代理，并且实现科学上网。

首先要有一台云服务器，比如买一台[阿里云](https://www.aliyun.com/)的，服务器位置当然要选个能为所欲为的。

只是测试的话可以弄个按量付费，最低配每小时不超过0.2元。不过需要账户余额>100元，余额可以随时提现。

搞定后，服务器端需要单开一个端口给代理用，可以在阿里云的安全组设置里开启，比如8888端口。

代理软件用极简的[shadowsocks](https://shadowsocks.org/en/index.html)，服务器端客户端都要安装。

客户端解压即用:

+ [shadowsocks-windows客户端](https://github.com/shadowsocks/shadowsocks-windows/releases)

+ [shadowsocks-Mac客户端](https://github.com/shadowsocks/ShadowsocksX-NG/releases)

服务器端走如下流程安装：

For CentOS 7.4:

	pip install --upgrade pip
	pip install shadowsocks

任意位置新建config.json，写入

	{
    "server":"内网IP",
    "server_port":8888,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"自定义密码",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
	}

运行服务：

	ssserver -c config.json

后台运行、重启、关闭：
	
	ssserver -c config.json -d start
	ssserver -c config.json -d restart
	ssserver -c config.json -d stop

服务器端配置完成了，后台运行的话可以放心退出了

客户端打开软件，服务器地址填入公网IP，服务器端8888，代理端口1080，密码自定义，其余不用填。

设置保存后，客户端状态栏右键启用系统代理，完成。

如浏览器依上文安装了SwitchyOmega插件，需要点系统代理模式。

开始上网吧。

完。