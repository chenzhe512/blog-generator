---
title: JS数据
date: 2018-07-23 11:01:56
tags:
---
>JS语言的每一个值，都属于某一种数据类型。一共有七种数据类型：Number、String、null、undefined、Boolean、Object、Symbol.
# 简介
1. Number: 数值即整数和小数；
2. String: 字符串即文本；
3. null: 表示空值，即此处的值为空；
4. undefined: 表示未定义，即目前没有定义，所以此处暂时没有任何值；
5. Boolean: 布尔值即表示真伪的两个特殊值，真(true)和伪(false);
6. Object: 对象，通常是三个原始类型的值的合成，可以看作是一个存放各种类型的容器；
数值、字符串、布尔值这三种类型是最基本的数据类型，所以称为JS的原始类型；而null和undefined是JS数据类型的两个特殊值；对象则称为合成类型，分为三个子类型object（狭义的对象）、数组（array）和函数（function）。
## 如何确定一个值是什么数据类型？
1. typeof运算符
2. instanceof运算符
3. Object.prototype.toString方法
***
# 详细了解各种数据类型
## null和undefined
null和undefined都可以表示‘没有’，含义基本相似。
null表示空值，即该处的值现在为空。如果调用函数时，某个参数未设置任何值，这时传入null，表示该值为空；
undefinde表示‘未定义’，返回为undefined的有：
```
//变量声明了，但没有赋值
var i;
i;//undefined
//调用函数时应该提供的参数没有提供，该参数就等于undefined
functionf(x){
    return x;
}
f()//undefined
//对象没有赋值的属性
var  o = new Object();
o.p //undefined
//函数没有返回值时，默认返回undefined
function f(){}
f()//undefined
```
## Boolean
布尔值只有true和false两个值。
如果JavaScript预期某个位置上是布尔值，会将该位置上现有的值自动转换为布尔值。转换规则是下面六个值转为false，其他值都是true：
undefined、null、false、0、NaN、''、""、document.all。
注：''和""都代表空字符，document.all不常用。
    详细查看 MDN falsy
## Number
### 概述
1. 整数和浮点数
在JavaScript中，所有数字都是以64为浮点数的形式储存的，整数也是如此。所以1与1.0是相同的代表同一个数。这就是说，在JavaScript的底层根本没有整数，都是以小数的形式即64位浮点数存在的。
2. 数值精度
JavaScript浮点数的64个二进制，从最左边开始是这样组成的：
第1位，符号位，0代表正数，1代表负数；
第2-12位，指数部分；
第13-63位，小数部分；
符号代表了一个数的正负，指数部分决定了数的大小，小数部分决定了数值的精度。