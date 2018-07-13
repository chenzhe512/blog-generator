---
title: CSS居中
date: 2018-06-28 16:24:56
tags:
---
# 布局
实现左右布局主要通过float: left; + clearfix 来实现的。即：
给子元素加float: left;
给父元素加clearfix;
其中
.clearfix::after{
    content: '';
    display: block;
    clear: both;
}



# 居中
## 水平居中
1. 学习后首先想到的水平居中的方法就只有width和margin的结合可以实现居中。
做常见的水平居中：给div定义一个宽度，然后配合margin的左右值为auto来实现效果；
```
div{
    width: 100px;
    margin: 0 auto;
}
```
方法简单易懂，浏览器兼容强，但扩展性差，就是说你在不知道width的情况下很难进行。
2. 在块级父元素中让行内元素居中，只需使用text-align: center;
`text-align: center;`
这种方法可以让inline/inline-blcok/inline-table/flex等类型的元素实现居中。
## 垂直居中
### 块级元素的垂直居中
如果说已知块级元素的高度：
```
.parent {
    position: relative;
    width: 300px;
    height: 300px;
    border: 1px solid red;
} 
.child {
    position: absolute; 
    top: 50%; 
    height: 100px; 
    margin-top: -50px;
    border: 1px solid red;
}
```

如果说未知块级元素的高度：
```
.parent{
  position: relative;
  height: 500px;
  width: 500px;
  border: 1px solid red;
}
.child{
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  border: 1px solid red;
}
```
### 行内元素的垂直居中
1. 文字的垂直居中只需将行高与高度设置为相等就可以实现。
```
div{
    height: 100px;
    line-height: 100px;
}
```
2. 可以通过给行内元素添加padding-top和padding-bottom来实现垂直居中。
# 补充
## 脱离文档流
position：fixd；可以让banner相对于屏幕固定，不占文档流的高度，即脱离文档流；
脱离之后文档流会缩起来，解决方法是：width: 100%;
使用width: 100%;之后会出现bug，左右100%+padding>父元素宽度
解决方法：左右边距变为0，这是宽度真的是100%，重新加一个div，即加给
topNavBar-inner,重新加之后，选择器和浮动都要重新更改；再给新加元素tipNavBar一个padding,因为这个padding是加在topNavBar-inner里面的，所以说宽度最多还是100%，不会超过父元素topNavBar的宽度。