---
layout: post
title: 'inline-block中设置margin影响同行元素的解决办法'
subtitle: ''
date: 2018-03-18
categories: 技术
tags: css
---
## inline-block中设置margin影响同行元素的解决办法

​	今天在做一个案例时遇到了一个问题,就是在同一行设置了display:inline-block属性的元素在设置margin属性是会影响全部元素.

​	例如目标状态为

![](http://p40uspzz2.bkt.clouddn.com/inline-block3.png)





​	初始状态为

```html
<div class="head">
			<div class="head-left fl">
				<a href="https://www.baidu.com/" target="_blank">百度网盘</a>
				<span>客户端下载</span>
			</div>
			<div class="head-right"></div>
		</div>
```



```css
.head-left a {

		width: 170px;
		height: 44px;
		background: url(../img/download-all.gif) no-repeat -643px 0px;
		margin: 10px 0 0 9px;
	}

	.head-left span {
		width: 76px;
		height: 25px;
		background: url(../img/download-all.gif) no-repeat -690px -60px;
	}
```

![](http://p40uspzz2.bkt.clouddn.com/inline-block1.png)

​	想让span下移，给span设置margin后

```css
.head-left span {
		width: 76px;
		height: 25px;
		margin-top: 20px;
		background: url(../img/download-all.gif) no-repeat -690px -60px;
	}
```

​	a元素和span同时下移

![](http://p40uspzz2.bkt.clouddn.com/inline-block2.png)

​	出现问题的原因:

​		在inline-block中设置margin肯定会影响同行元素，因为它们存在某种对齐方式(一般默认为vertical-align: baseline 基线对齐)。

​	解决办法:

​	1.使用定位(不推荐,不好维护)

​	2.设置vertical-align: middle后再设置margin

```css
.head-left a {
		width: 170px;
		height: 44px;
		background: url(../img/download-all.gif) no-repeat -643px 0px;
		margin: 10px 0 0 9px;
		vertical-align: middle;
	}
	.head-left span {
		width: 76px;
		height: 25px;
		vertical-align: middle;
		margin-top: 18px;
		background: url(../img/download-all.gif) no-repeat -690px -60px;
	}
```

![](http://p40uspzz2.bkt.clouddn.com/inline-block3.png)

参考资料:https://segmentfault.com/q/1010000003750187

扩展:[张鑫旭对css-vertical-align的一些理解与认识](http://www.zhangxinxu.com/wordpress/2010/05/%E6%88%91%E5%AF%B9css-vertical-align%E7%9A%84%E4%B8%80%E4%BA%9B%E7%90%86%E8%A7%A3%E4%B8%8E%E8%AE%A4%E8%AF%86%EF%BC%88%E4%B8%80%EF%BC%89/)