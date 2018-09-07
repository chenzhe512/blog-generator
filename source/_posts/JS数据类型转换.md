---
title: JS数据类型转换
date: 2018-07-23 14:25:30
tags:
---
本文主要介绍JS中数据的类型转换。
# 转换为字符串
String()可以把任意类型的值转换为字符串。
## 原始类型值
1. 数值：转换为相应的字符串；
2. 字符串：转换后还是原来的值；
3. 布尔值：true转为字符串'true'，false转为字符串'false'；
4. undefined：转为字符串'undefined'；
5. null：转为字符串'null'；
## 对象
Sting()方法的参数如果是对象，返回一个类型字符串；如果是一个数组，返回该数组的字符串形式；
```
String([1, 2, 3])
"1,2,3"
String({a: 1})
"[object Object]"
```
注：如果是数值和布尔类型的还可以通过number/boolean + ''或者'' + number/boolean来进行转换；
window.String()也可以转换为字符串。
# 转换为布尔
Boolean()函数可以将任意类型的值转换为布尔。
除了undefined、null、0、NaN以及空字符串的转换结果为false，其他全都为true。
注： 也可通过!!()来进行转换。
# 转换为数值
Number()函数可以将任意类型的值转换为数值。
## 原始类型的值
1. 数值：转换后还是原来的值；
2. 字符串：如果可以转换为数值，则直接转换为数值；如果不能转换为数值，则直接返回NaN；空字符串转换为0；
3. 布尔值： true转换为1，false转换为0；
4. undefined：转换为NaN；
5. null：转换为0；
注： 还可通过parseInt()和parseFloat()转换为Number；
'1' - 0和+ '-1' 也可以转换为数值。
