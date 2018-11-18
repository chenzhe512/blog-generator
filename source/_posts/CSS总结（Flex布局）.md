---
title: CSS总结（Flex布局）
date: 2018-11-12 18:36:53
tags:
---
> Flex布局。

## 之前的布局如何实现
1. normal flow（正常流/文档流）
2.  float + clear
3. position relative + absolute
4. display inline-block
5. 负 margin
## 
(基本概念)
(属性)
+ flex-direction
column、row、column-reverse、row-reverse
+ flex-wrap(换行)
wrap
+ flex-flow
上面两个的简写 fle-flow: row wrap;
+ justify-content
主轴方向对齐方式
space-between、space-round、flex-start、flex-end、center
+ align-items
侧轴对齐方式
stretch(所有元素伸开)、flex-start(所有元素往侧轴起点靠)、flex-end(终点靠)、center
+ align-content
多行列内容对齐方式
stretch、space-between、space-round、flex-start、flex-end

------------
## flex item
flex-grow 分配多余空间
flex-shrink 收缩空间
flex-basis 默认大小（不用）
flex 前面三个缩写
order 顺序（代替双飞翼） 该CSS改展示顺序
flex-self 分配每一个自己的顺序自身的对齐方式


overflow: auto;



------------------------------------------------

# 布局套路
+ 原则
不到万不得已，不要写死 width 和 height
尽量用高级语法，如 calc、flex
如果是 IE，就全部写死
## 浮动布局
### float
儿子全加 float: left （right）
老子加 .clearfix
-----
导航右边要靠边：
不要给右边只给左边
margin-left: 20px;
--------
左边logo 高度为36px，右边导航给个line-height:24px;
如何实现logo与右边导航的对齐？
只需要给导航一个padding，达到36px即可。
-----------
单行文字居中方法？
设置line-height和height一样，常用单行文字居中方法。
--------------
拉倒一定程度布局乱了？
设置min-width: 600px; 
小到一定程度出现滚动条。
---------------------------
IE6？
.clearfix:after{
    content: '';
    display: block;
    clear: both;
}
.clearfix{
    zoom: 1;
}
### float做平均布局
+ 第一种
```
.picture:nth-child(4n+1){
  margin-left:0;
}
.picture:nth-child(4n){
  margin-right:0;
}
```
+ 第二种
在pictures和picture中间加一个div.middle
负margin
```
.pictures > .middle{
  margin-left: -4px;
  margin-right: -4px;
}
```
### flex做平均布局
```
display:flex;
flex-wrap:wrap;
justify-content:space-between;
```
如果说不是8个，是7个呢，这样会显示bug，导致第二行的3个div中间空隙过大？
解决办法依然是负margin和div.middle
```
.pictures > .middle{
  display: flex;
  flex-wrap: wrap;
  margin: 0 -4px;
}
.picture{
  width: 194px;
  height: 194px;
  background: red;
  margin: 4px;

}
```

------------
用calc
```width: calc(25% - 8px);```

------------
重要：用作布局的div不要在上面加其他东西，只能用作布局，否则容易bug。

```
.art > .sider{
  width: calc(33.333333333% - 20px);
  margin-right: 20px;
}
```
用calc减20px，加在margin-right上。

-----------------
## 移动布局
1. 第一步
```
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  ```
删除min-width
overflow:hidden;
怕图片变形，不要用img标签，用background等。size
如果一定要图片1:1显示，请搜索  固定比例div