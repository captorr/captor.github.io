---
layout: post
title: "ggplot2双轴,双y轴"
date: 2018.06.07 14:29
categories: R
tag: plot
---
* content
{:toc}


帮洁哥画图时遇到个问题，问题本身比较复杂，简化一下变成了加双坐标轴的问题。曾经的ggplot2是不能完美画出双轴的，而且不完美的方法也是简直土到爆炸，强行用annotation或者图层硬叠的办法，很容易出现遮盖或者修改一点点东西都要大费周章还不一定解决的问题。于是我都要放弃用R画的时候，突然get到了新技能，ggplot2 2.2.0版本新增加了sec.axis()方法可以直接增加第二坐标轴，果然技能不能一直吃老本，总要抛弃些过气的认知，适时掌握新方法。2.2.0是16年底更新的，距今也有1年半了，总是感觉没多久的样子。

## 画个锤子

sec.axis()的文档：[Specify a secondary axis](http://ggplot2.tidyverse.org/reference/sec_axis.html#arguments)

sec.axis()要放在scale\_x/y\_continuous()里使用, 参数示例sec_axis(trans = NULL, name = waiver(), breaks = waiver(), labels = waiver())。

trans是一个转换公式，用来将双轴的值域统一，~.后可接公式，大概是“轴1=~.xxx轴2”，比如轴1的值域是0-10，轴2的值域是5-75，则xxx等于(10-0)/(75-5)=1/7，可表示为~./7或者~.*0.142857。同理也可用其他线性、非线性的公式转换值域。name是轴标签，breaks、labels是刻度位置、标签，道理等同。

举个实际代码的例子：

	\+scale_y_continuous(name='',breaks=lable.site1,label=names(lable.site1),sec.axis=sec_axis(~.*1,breaks=lable.site2,labels=names(lable.site2)))


之后还会遇到一个问题，如何分别调整双轴轴标签、刻度标签的属性？

可在theme中用axis.text.y=element_text()同时调整两轴，用axis.text.y.right=element_text()单独调整副轴。

举个实际的例子：

	\+theme(axis.text.y=element_text(size=rel(0.85)),axis.text.y.right=element_text(size=rel(1.3)))

以上代码将主轴刻度标签调整为0.85倍主题大小，副轴调整为1.3倍主题大小。


一个示例图：

![Rhc9u.png](https://s1.ax2x.com/2018/06/07/Rhc9u.png)


双x轴也是同样的道理，没了。