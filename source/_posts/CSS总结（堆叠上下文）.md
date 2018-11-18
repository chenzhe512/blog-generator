---
title: CSS总结（堆叠上下文）
date: 2018-11-09 01:35:21
tags:
---
> 堆叠上下文。

## 问题
```
div{
  width: 200px;
  height: 200px;
  border: 5px solid red;
  padding: 12px;
  margin: 15px;
  background-color: black;
}
```
### border与background相比，哪个更靠近你的眼睛。
border
确定方法：```border: 5ps solid rgba(255,0,0,1);```
### border与文字（内联元素）相比，哪个更靠近你的眼睛？
确定方法：```text-indent: -20px;```
### div(块级元素)与文字（内联元素）相比,哪个更靠近你的眼睛？
确定方法：```margin-top: -15px;```
```
.parent{
  width: 200px;
  height: 200px;
  border: 5px solid red;
  padding: 12px;
  margin: 15px;
  background-color: black;
}
.child{
    height: 20px;
    backgrond: purple;
    margin-top: -15px;
}
```
### 文字先出现与后出现，哪个？
后出现的离用户眼睛更近。（块级元素也是如此）
```
.parent{
    color: red;
}
.child{
    color: black;
}
```
inline-block元素与内联元素相同。
### 浮动？
处于内联元素与块级元素之间。
所以浮动元素内的文字比内联元素中的文字低。
### 相对定位元素
```position:relative;```
最高的
z-index只能给定位元素加。
```
.relative1{
    width: 100px;
    height: 100px;
    background: orange;
    position: relative;
}
.relative2{
    width: 100px;
    height: 100px;
    background: green;
    position: relative;
}
```
如果两个都是相对定位，后出现的盖住先出现的（离用户眼睛更近）.
z-index默认auto，如果给.relative加```z-index: 1;```他会盖住relative2.
如果两个都是```z-index:1;```,relative2会盖住relative1，因为后出现的是relative2.
```position:absolute;```与```position:relative;```的三种情况都是如此。
## 堆叠上下文
在父元素上绝对/相对定位之后，并且z-index不是auto。
MDN
## 堆叠上下文对z-index的影响
