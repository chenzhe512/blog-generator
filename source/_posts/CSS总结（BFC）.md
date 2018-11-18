---
title: CSS总结（BFC）
date: 2018-11-13 15:03:18
tags:
---
> BFC.

## MDN 对于BFC的定义
一个块格式化上下文（block formatting context） 是Web页面的可视化CSS渲染出的一部分。它是块级盒布局出现的区域，也是浮动层元素进行交互的区域。

一个块格式化上下文由以下之一创建：

+ 根元素或其它包含它的元素
+ 浮动元素 (元素的 float 不是 none)
+ 绝对定位元素 (元素具有 position 为 absolute 或 fixed)
+ 内联块 (元素具有 display: inline-block)
+ 表格单元格 (元素具有 display: table-cell，HTML表格单元格默认属性)
+ 表格标题 (元素具有 display: table-caption, HTML表格标题默认属性)
+ 具有overflow 且值不是 visible 的块元素，
+ display: flow-root
+ column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中。
一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。

块格式化上下文对于定位 (参见 float) 与清除浮动 (参见 clear) 很重要。定位和清除浮动的样式规则只适用于处于同一块格式化上下文内的元素。浮动不会影响其它块格式化上下文中元素的布局，并且清除浮动只能清除同一块格式化上下文中在它前面的元素的浮动。

## 属性
唯一一个触发BFC的属性display:flow-root;
其他什么都不会触发。
一旦是BFC就有一个功能：
将它内部的浮动元素包括住。
第二个动能：
功能2：兄弟之间划清界限
用 float + div 做左右自适应布局


margin合并

float:left;和overflow:auto;配合实现浮动布局。还可以其他的值。
如果用两个float:left;的话会导致didi不能自适应。