---
layout: post
title: "一个google翻译模块"
date: 2018.04.17 15:37
categories: scripts
tag: scripts
---
* content
{:toc}


某些情况下，自动翻译的需求还真是意外的高，虽然不可能100%准确意味着翻译结果都要人工校正，不过需求还是很大啊。曾经写过一个脚本帮助翻译短句，当时随便找了个轮子试了一下能用就用了，是这个模块[googletrans](https://github.com/ssut/py-googletrans)。前段时间开两会网络和谐了一段时间，发现个问题，这模块居然要翻墙才能用，这特么就很尴尬了，虽然翻了墙还是能用，但是单纯的google translate服务也不需要翻墙啊。于是决定自己搞一个脚本试试。

## 俺耶格今天要爆了你的狗头

今天俺要搞个不需要翻墙的google翻译脚本。

首先打开一个google翻译的页面，随便翻译点东西试试。能用，很正常，没啥毛病。可以发现翻译后的网址都变了，后面多了一大串字符串。仔细分析一下，没错，这就是刚刚翻译的内容，标点符号用了html编码替换而已。

试一下把要翻译的内容拼成字符串当做URL直接用get或者post方法试试。

不用想了，果然不行。

老老实实抓包看一下，原来URL不是<font color='#FF3333'><del>弱智一般地</del></font>拼接就可以的。而是这个：

https://translate.google.cn/translate_a/*


![841qY.png](https://s1.ax2x.com/2018/04/25/841qY.png)

需要几个参数，其他的看起来好像很简单，比较奇怪的是tk和q这两个参数，q肯定是要翻译的内容了，tk是个啥啊。不管了，先照着填进去试试。

![84I2X.png](https://s1.ax2x.com/2018/04/25/84I2X.png)

翻译原句有结果了~

换了个句子果然不行了。

![84kzl.png](https://s1.ax2x.com/2018/04/25/84kzl.png)


看来tk是个和字符串相关联的东西。查查吧。

真的搜到了[一个博客](https://blog.csdn.net/yingshukun/article/details/53470424)，而且经历了和我一样的心路历程，看来轮子不用自己造了。

TK的算法也有大神研究过：[Google_TK](https://github.com/cocoa520/Google_TK/blob/master/google_tk.html)

不过是html格式的，看起来不太适合我们，而且看这意思还是js算的，所以依博主意思用一个模块把这html里写的js函数在python里搞成我们能直接用的就行了。反正python就擅长干这个。

模块博主也给了：[ExecJS](https://github.com/doloopwhile/PyExecJS)

好像没说支持pyhton 3.6。不过还是试一试吧。

pip install 一下

![848lB.png](https://s1.ax2x.com/2018/04/25/848lB.png)

大概是装好了吧。<font color='#FF3333'><del>pip版本问题就不要在意了，什么都没看见。</del></font>

测试一下，一次通过了。

居然这就完了。俺耶格还没...

感谢各位的轮子，很好用，五星好评。

修剪一下脚本，留着备用。
