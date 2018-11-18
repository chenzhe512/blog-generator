---
title: CSS总结（动态REM）
date: 2018-11-13 16:06:13
tags:
---

> REM.
```
html{
    font-size:20px;
}
p{
    font-size:2em;
}
```
rem是根元素的font-size
em是自己的font-size


+ 百分比布局
高度很难。不确定性太多。
vw兼容性太差。
+ 动态REM
```
<script>
    var pageWidth = window.innerWidth
    document.write('<style>html{font-size:' + pageWidth/10 + 'px;}</style>')
  </script>
```
用rem模拟vw

先/100   然后*100

scss



##  表单美化
3个
```
.inputWrapper input[type=text]:focus{
  outline:none;
  border-color:#4b94fc;
}
```
```outline:none;```去除focus时的颜色。
 vertical-align:top; 去除图片下面的空隙。

 图片上传

 display none 不能做动画