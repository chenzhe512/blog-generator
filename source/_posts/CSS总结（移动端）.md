---
title: CSS总结（移动端）
date: 2018-11-12 15:14:00
tags:
---
> CSS之移动端。

## 媒体查询
```
    <style>
        @media (max-width: 800px){
            body{
                background: red;
            }
        }
    </style>
```
如果想在不同的设备显示不同的颜色怎么写？
+ ```@media (max-width: 320px)```
+ ```@media (max-width: 375px)```
+ ```@media (max-width: 425px)```
+ ```@media (max-width: 768px)```
+ ```@media (min-width: 769px)```
这样写会导致最终显示768px的那种CSS页面。因为是写的0~320px，0~375px...
后面的优先级会比前面的高，会覆盖掉前面的格式。
解决方法：
1. 倒着写
```
@media (min-width: 769px)
@media (max-width: 768px)
@media (max-width: 425px)
...
```
2. 写明确
```
@media (max-width: 320px)
@media (min-width: 321px) and (max-width: 375px)
@media (min-width: 376px) and (max-width: 425px)
...
```
## 媒体查询外联CSS文件
```
<link rel="stylesheet" href="style.css" media="(max-width: 320px;)">
```
这个style.css文件始终都会下载，但只在屏幕小于320px时才会生效。

响应式页面案例：[案例](https://www.smashingmagazine.com/)

```
 ul>li*5>a[href=#]{导航$}

         <ul>
            <li><a href="#">导航1</a></li>
            <li><a href="#">导航2</a></li>
            <li><a href="#">导航3</a></li>
            <li><a href="#">导航4</a></li>
            <li><a href="#">导航5</a></li>
        </ul>
```

```
       ul>li>a[href=#]{导航$}*5

        <ul>
            <li>
                <a href="#">导航1</a>
                <a href="#">导航2</a>
                <a href="#">导航3</a>
                <a href="#">导航4</a>
                <a href="#">导航5</a>
            </li>
        </ul>
```

## 手机端点击按钮出现li导航栏
+ 第一种（不推荐）
```
    <script>
        xx.onclick = function(){
            if(yy.style.display === 'block'){
                yy.style.display = 'none'
            }else{
                yy.style.display = 'block'
            }
        }
    </script>
```
不要去该一个元素的style,去更改这个元素的class
+ 第二种（推荐）
```
.nav{
    display: none;
}
.nac.active{
    display: block;
}
```
```
xx.onclick = function(){
    yy.classList.toggle('active')
}
```

-----------------------
让按钮在右边：
```
        header > button{
            float: right;
        }
```
        header{
            position: relative;
        }
        header > button{
            position: absolute;
            top: 0;
            right: 0;
        }
```
用了dis:flex;
.clearfix就可以去掉了，自动排版。

```    
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```


1. 没有hover
2. 有touch事件（jquery swiper/ vue swiper),不去监听click事件
3. resize没有
4. 没有滚动条