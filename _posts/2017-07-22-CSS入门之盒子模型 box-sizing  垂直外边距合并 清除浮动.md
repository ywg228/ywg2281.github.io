---
layout:     post
title:      CSS入门之盒子模型 box-sizing 垂直外边距合并 清除浮动
subtitle:   CSS入门
date:       2017-07-22
author:     Ywg
header-img: img/home-bg-o.jpg
catalog:    true
tags: CSS CSS入门
---

## 前言
- CSS盒子模型：在一个文档中，每一个元素都被抽象成一个盒子。
- 盒模型从内到外由四部分组成：content内容、padding内边距、border边框和margin外边距。
- 盒模型是区分方向的：上右下左。

![盒模型](http://static.oschina.net/uploads/img/201503/10153449_ZoQu.png)

而盒模型包括W3C标准盒模型和IE盒模型。

## W3C标准盒模型
- 盒子的大小就是content的大小，不包括padding和border。
``` 
width = content-width 
height = content-height
``` 
- 通过JavaScript代码获取某一个元素的大小时，所得到的width和height其实是盒子模型中的content的大小。

![标准盒模型](http://clover.htmhub.com/img/201503151.JPG)

## IE盒模型
- IE盒模型与标准盒模型的核心差异是：IE盒模型的盒子大小包含了border和padding。
``` 
width = content-width + padding-width + border-width
height = content-height + padding-height + border-height
``` 
![IE盒模型](http://clover.htmhub.com/img/201503152.JPG)

##  box-sizing
这是CSS3的一个属性，它的默认值是 content-box ，也就是标准盒模型。如果将它设置为 box-sizing: border-box ，浏览器会使用IE盒模型渲染页面，即 width 和 height 属性将包含边框和内边距。
- content-box：w3c标准盒模型
- border-box：IE盒模型

![box-sizing](http://clover.htmhub.com/img/2406284-6a337b312349eb87.png)

元素的内边距和边框不再会增加它的宽度，如下两个盒子宽度一样都为500px
```
.box1 {
  width: 500px;
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}

.box2 {
  width: 500px;
  border: 10px solid blue;
  padding: 50px;
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
```

## 垂直外边距合并
- 在文档正常流中，当两个元素框的垂直外边距相遇时，它们将形成一个外边距。
- 合并后的外边距的高度等于两个发生合并的外边距高度中的较大者。

1. 当一个元素出现在另一个元素上面时，第一个元素的下外边距与第二个元素的上外边距会发生合并。
如下图所示：

![外边距合并](http://songziming.com.cn/2016/12/16/CSS-box-model/3.png)

2. 当一个元素包含在另一个元素中时（假设没有内边距或边框把外边距分隔开），它们的上和下外边距也会发生合并。
如下图所示：

![外边距合并](http://songziming.com.cn/2016/12/16/CSS-box-model/4.png)

3. 外边距甚至可以与自身发生合并，假设有一个空元素，它有外边距，但是没有边框或内边距。在这种情况下，上外边距与下外边距就碰到了一起，它们会发生合并：

![外边距合并](http://songziming.com.cn/2016/12/16/CSS-box-model/5.png)

4. 如果这个外边距遇到另一个元素的外边距，它还会发生合并：

![外边距合并](http://songziming.com.cn/2016/12/16/CSS-box-model/6.png)

5. 外边距合并既能够节省页面空间又能使页面更加美观。

![外边距合并](http://songziming.com.cn/2016/12/16/CSS-box-model/7.png)


#### 注意
- 只有 **普通文档流** 中 块框 的 **垂直外边距** 才会发生外边距合并。
- 行内框、浮动框或绝对定位之间的外边距不会合并。
- 所有元素的内边距、边框以及水平外边距也都不会合并。

## 浮动及清除
#### 问题
在使用了浮动float后，使用浮动的元素溢出到了父容器外面！父容器并没有撑开！

#### 原因
浮动元素脱离了原来的文档流，不受父元素的控制。我们就需要让父元素包含浮动的子元素。

#### 解决
给父元素添加一个非浮动的子元素，然后清除该子元素。在浮动元素的父容器加上clearfix即可。
```
.clearfix:after {
  content: ".";
  display: block;
  height: 0;
  clear: both;
  font-size: 0;
  visibility: hidden;
}
.clearfix {
  *zoom: 1; /* For IE 6&7 only 可省略*/
}
```

## 资料
[学习CSS布局](http://zh.learnlayout.com/toc.html)
