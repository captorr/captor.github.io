---
layout: post
title: "Jekyll搭建个人博客——从入门到放弃"
date: 2018.01.03 16:40
categories: jekyll
tag: tech
---
* content
{:toc}


## 啥是Jekyll

<font color="#FF3300">我也不知道。</font>

Jekyll是Github上的一个开源项目，简单轻量，对文本的处理非常灵活友好，并且提供了傻瓜打包式的安装搭建教程，加上无数中文贡献者的无私答疑建设，模板QA之类的多到看不过来，总之十分适合 <font color="#FF3300"><del>零基础or懒or真的就是笨</del></font> 愿意折腾的geeker<font color="#3399FF">们</font>拿来用作个人博客的框架。

Jekyll同时也是Github Pages的引擎之一，可以直接在Github上通过建repository的方式变出一个博客网页，通过push代码的方式更新博客，简直方便。<font size=2>当然，这个方便是Github Pages的方便，换个框架也可以变出个网页。</font>

+ Jekyll项目Github地址: [https://github.com/jekyll/jekyll](https://github.com/jekyll/jekyll)

项目介绍是这么说的

>Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. Think of it like a file-based CMS, without all the complexity. Jekyll takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server. Jekyll is the engine behind GitHub Pages, which you can use to host sites right from your GitHub repositories.

## 我都干了啥

<font color="#FF3300">去年</font>fork了这个简单版的框架： [Jekyll Clean](https://github.com/scotte/jekyll-clean) ，[博客地址](https://github.com/scotte/jekyll-clean)

今年fork了这个强化版的框架： [maoxiaoke.github.io](https://github.com/maoxiaoke/maoxiaoke.github.io)，[博客地址](http://xiaokedada.com/)

首先点个星，然后fork，再然后clone到本地给respository换个名字，换成captorr.github.io的话就可以直接在[captorr.github.io](http://captorr.github.io)网址打开了。接下来将原主的个人信息修改成自己的信息，相关代码例如计数评论等与原项目主分离以免相互影响。

基于原项目做了些弱化修改。[maoxiaoke](https://github.com/maoxiaoke/maoxiaoke.github.io)的博客主页的动态效果感觉很好看，我拿到本地后通过jekyll serve能看到动态效果，但是放到Github上以后效果就没了。检查之后发现是Github不支持一些js脚本的HTTP地址解析造成的，把HTTP改成HTTPS之后问题解决。修改的文件位置是./_includes/docs_header.html。

在这之前，我对Jekyll可谓一无所知，主要参考了这些资料：

+ [jekyll官网](https://jekyllrb.com/)

+ [用 Github + Jekyll 写博客](http://blog.csdn.net/u014015972/article/details/50497254)

+ [基于Jekyll静态框架的Github站点设计](http://xiaokedada.com/2017/02/22/Jekyll-Cpanel/)

自己动一遍手当然是最容易解决问题的办法，其中有一些小问题，有机会可以详细描述一下。总体而言，从零开始首先是理解jekyll框架工作机制，然后是寻找合适的模板，再然后对模板调整，顺便学一下markdown语法直接开写就可以了。<font color="#FF3300"><del>当然这个0说的是jekyll的0。</del></font>







