---
title: CSS总结（第一部分）
date: 2018-11-08 22:58:57
tags:
---
> CSS总结。

### 实现内联元素的两端对齐：
```
<style>
    span{
      border: 1px solid red;
      display: inline-block;
      width: 100px;
      text-align: justify;
      line-height: 20px;
      over-flow: hidden;
      height: 20px;
    }
    span::after{
      content: '';
      display: inline-block;
      width: 100%;
    }
    在姓名下方另起一行，撑起宽度，然后隐藏。
```
```
<span>姓名</span> <br>
<span>联系方式</span>
```
### inline元素中间的空格
```
 <ul>
   <li>选项1</li>
   <li>选项2</li>
   <li>选项3</li>
   <li>选项4</li>
   <li>选项5</li>
 </ul>
```
```
<style>
  ul {
    padding: 0;
    margin: 0;
    list-style: none;
  }
    ul > li{
      display: inline-block;
      border: 1px solid red;
    }
  </style>
```
inline-block元素还是inline元素 中间的换行都会出现空格，如何没有空格
```
ul {
    padding: 0;
    margin: 0;
    list-style: none;
    border: 1px solid red;
  }
    ul > li{
      float: left;
      border: 1px solid red;
    }
    .clearfix::after{
      content: '';
      display: block;
      clear: both;
    }


<ul class="clearfix">
   <li>选项1</li>
   <li>选项2</li>
   <li>选项3</li>
   <li>选项4</li>
   <li>选项5</li>
 </ul>
```
### 文字溢出省略号（div中）
#### 一行文字溢出
``` word-break: break-all;```
字面理解就是可以把一个词打开，哪里都可以。
```white-space: nowrap;```
可以阻止文字换行。
```text-overflow: ellipsis;```
```
  div{
    border: 1px solid red;
    white-space: nowrap;
    overflow:hidden;
    text-overflow: ellipsis;
    
  }
```
#### 多行文字溢出
直接搜索css multi line-text ellipsis
```
  div{
    border: 1px solid red;
    display: -webkit-box;
    -webkit-line-clamp: 2;                    //显示几行
    -webkit-box-orient: vertical;
    overflow: hidden;                         //多余隐藏
    
  }
```
### 文字垂直居中（div中）
小白写法：
```
div{
    border: 1px solid red;
    height: 40px;
    line-height: 40px;
}
```
正确写法：
```
div{
    border:1px solid red; //border占据空间，可以用outline不占据空间。
    line-height: 24px;
    padding: 8px 0;
    text-lign: center;
}
```
水平居中直接text-align：center；
这样写的好处在于无论文字多少 不会出现bug（排版混乱的问题）。
### margin合并问题
```
  .dad{
    border: 5px solid red;

  }
    .son{
      border: 10px solid black;
      line-height: 40px;
      padding: 20px;
    }
```
这样洗，只要.son加line-height或者padding,.dad都会撑大。
如果给.son加一个`margin: 10px ;`后,.dad会不会被撑大呢。
答案： 不会。
这是因为.son和.dad的margin合并
```
  .dad{
    outline: 5px solid red;

  }
    .son{
      border: 10px solid black;
      padding: 20px;
      margin: 10px;
    }
```
如何解决这个问题
+ 加border-top、border-bottom
+ padding-top、padding-bottom
+ overflow: hidden;(不推荐
)
+ 写一个字（内联元素）
就不会合并margin
### div高度
div高度由内部文档流元素高度的总和决定的。
文档流，文档流中内联元素从左到右依次排列，不够换行，块级元素从上到下。
#### 脱离文档流(算高度的时候别叫上我)
+ float: left;
+ position: absolute;
+ position: fixd;
position: absolute;不会脱离文档流。
#### div中的div如何垂直居中
```
    .dad{
      outline: 1px solid green;
      padding: 100px 0;
    }
    .son{
      border: 5px solid black;
      width: 200px;
      padding: 10px;
      margin: 0 auto;
    }
```
父元素中加上下padding可以实现上下居中；
子元素中加```margin: 0 auto;```可以实现水平居中。
+ 高度宽度确定实现：
```
    .dad{
      outline: 1px solid green;
      padding: 100px 0;
      box-sizing: border-box;
    }
    .son{
      border: 5px solid black;
      width: 200px;
      padding: 10px;
      margin: auto;
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      heigt: 200px;
    }
```
```margin: auto;```配合定宽定高是可以实现的。
+ 高度宽度不能确定
```
.dad{
      border: 1px solid green;
      padding: 100px 0;
      box-sizing: border-box;
      display: flex;
      justify-content:center;
      align-items: center;
    }
.son{
    border: 5px solid black;
    padding: 10px;
    heigt: auto;
}    
```
主要加三句
```
display:flex;
justify-content:center;
align-items: center;
```
如何写一个1:1的div
```
.one{
    padding-top: 100%;
}
```