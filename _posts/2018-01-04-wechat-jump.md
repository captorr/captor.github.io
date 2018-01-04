---
layout: post
title: "用python玩微信跳一跳"
date: 2018.01.04 16:40
categories: python
tag: scripts
---
* content
{:toc}


2017年末微信上线了新版本<font color="#3399FF">(也就是前几天)</font>，同时更新了一个<font color="#3399FF"><del>一点都不</del></font> 好玩的小游戏，跳一跳。本着万年不更新软件的原则，我自然是不知道这玩意的存在的。不过老婆睡前让我帮她玩了一下下这个一点都不好玩的小游戏，然后第二天我就跟着更新了微信版本。。

手动玩个几百分还是很容易的，果不其然，用python的小伙伴们第一时间就搞出了电动版的脚本，简单粗暴地肆虐朋友圈。

<font color="#FF0033">所以我们也要加入。</font>

## 找个轮子

当时还不火（2017.12.30），今天却火到爆的（2018.01.04）python代码来源：

[教你用Python来玩微信跳一跳](https://zhuanlan.zhihu.com/p/32452473)

介绍了一个及其简单易懂的思路：

+ 截个图
+ 算下像素距离，已知距离正比于按压力度
+ 按照计算好的力度模拟按压
+ 意外死亡发个朋友圈

同时，也准备了一整套的起飞代码

[wangshub的Github项目地址](https://github.com/wangshub/wechat_jump_game)

我fork了一个去年的版本，不过今天看看也没啥太大变化。

## 材料准备

现在说说去年我是怎么玩这个游戏的。。。

首先，这个脚本需要依赖这么几个东西：

+ adb 工具包，实测有一些不好用的版本，我下的是[adb 10.0.32](http://ftp-idc.pconline.com.cn/7693126783c78c3af51339fad1873f9e/pub/download/201010/adb1.0.32.zip)不知道有没有毒，反正已经用了
+ python 2.7，链接就不放了。
+ 项目里[requirements.txt](https://github.com/wangshub/wechat_jump_game/blob/master/requirements.txt)里的python包
+ 一个安卓手机，装好微信，能玩跳一跳，有开发者模式

脚本我用的是改进版的[wechat_jump_auto.py](https://github.com/wangshub/wechat_jump_game/blob/master/wechat_jump_auto.py)，
脚本改好后连上手机，找好自己的屏幕分辨率，根据分辨率设置一下脚本里的参数就行了。

参数我设置的是：

+ press_coefficient = 1.04
+ piece_base_height_1_2 = 26
+ piece_body_width = 110

win7 and win10下都已经测试过了，可以完美运行。

## 开始玩吧

简单的试了一下，确实能动。不过很耗时间，一步5秒吧，可能我电脑的CPU太弱了。

晒一下去年的记录
![WAwVG.jpg](https://s1.ax2x.com/2018/01/04/WAwVG.jpg)

基本上可以完美跳中心，个别图形有失常，一共开了两次挂，上周3334，这周2828，两次的死因都是老婆凑过来看了一眼，然后莫名其妙就死了。。不知道是不是玄学。（逃）

## 第二次测试

今天又在公司电脑上试了一下这个脚本，还能用，分数上传的时候提示网络问题，上传不了。原项目[ISSUE](https://github.com/wangshub/wechat_jump_game/issues?page=14&q=is%3Aissue+is%3Aopen)里已经开始集中反思了，结论竟有可能是封号？！我差点就信了，然后玩到几百分后，手动跳了几下送死，分数上传成功了。

令人惊叹的是今天重看了原来的项目，这STAR,FORK数量都要上天了。电动脚本比原项目还吊的存在基本上是要凉的，所以想尝试脚本的还是尽快吧。