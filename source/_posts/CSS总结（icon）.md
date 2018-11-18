---
title: CSS总结（icon）
date: 2018-11-09 15:38:52
tags:
---

## PS切图
PS切出3个icon图 后，
3个 img标签搞定
## background icon 
与PS切图相比，不会变形
```
 <div class="icons" style="text-align: center;">
    <div class="icon qq"></div>
    <div class="icon weixin"></div>
    <div class="icon weibo"></div>
  </div>
```
```
  .icons > .icon{
    margin: 0 25px;
    border: 1px solid red;
    display: inline-block;
    width: 100px;
    height: 100px;
    background: transparent url(./qq.png) no-repeat 0 0;
  }
    .icons > .icon.qq{
      background-image: url(./qq.png);
    }
    .icons > .icon.weixin{
      background-image: url(./weixin.png);
    }
    .icons > .icon.weibo{
      background-image: url(./weibo.png);
    }
```
## CSS Sprites
google CSS sprite generator
原理： 展示你想要看到的
## iconfont

HTML:
```
<div class="xxx" style="font-family: iconfont;">
&#xe613;&#xe614;
<div>
<style>
@font-face {
    ...
}
</style>
```
&#xe6
之后的
字体
+ 伪类表示：
.xxx::before{
    content: '\e614';
}

----------

CSS:
自动生成：Font class
```
<link rel="stylesheet" href="" >
<span class = "iconfont icon-qq" ></span>
<span class = "iconfont icon-weixin" ></span>
<span class = "iconfont icon-weibo" ></span>
```

JS:
svg

## css法
cssicon.space
