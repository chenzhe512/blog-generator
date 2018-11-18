---
title: This
date: 2018-09-07 01:56:19
tags:
---
> this是JavaScript中的一个关键词。

# this概念
this是函数运行时，在函数内部自动生成的一个对象，只能在函数内部使用。
函数的不同场合，this的值也不同。但总的来说this就是函数运行时所在的环境对象。
JS函数可以在不同的环境中运行，所以需要有一种机制，能够在函数体内部获得当前的运行环境。所以，this就出现了，它的设计目的就是在函数体内部，指代函数当前的运行环境。
# 使用场合
## 全局环境
在全局环境中使用this，指向顶层对象window。(任何函数体外部)
```
this === window // true

a = 37;
console.log(window.a); // 37
```
## 构造函数
构造函数是通过这个函数可以生成一个新对象。此时，this指向正在构造的新对象（实例对象）。
简单介绍一下构造函数：
典型的面向对象编程语言（比如 C++ 和 Java），都有“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript 语言的对象体系，不是基于“类”的，而是基于构造函数（constructor）和原型链（prototype）。
构造函数的特点有两个：
+ 函数内部使用了this关键字，代表所有生成的实例对象。
+ 生成对象的时候，必须使用new命令。
构造函数的命令原理：
1. 创建一个空对象，作为将要返回的对象实例。
2. 将这个空对象的原型，指向构造函数的prototype属性。
3. 将这个空对象赋值给函数内部的this关键字。
4. 开始执行构造函数内部的代码。
```
function People(){
    this.name = '小明'
}
var a = new People()
console.log(a.name) //小明
```
## 对象的方法
对象的方法里面包含this，this的指向就是方法运行时所在的对象。该方法赋值给另一个对象，就会改变this的指向。
```
var a = {
    age: 22,
    getage: function(){
        return this.age
    }
}
console.log(a.getage()) // 22
```
a.getage方法执行时，内部的this指向a。

-----------------------

如果this所在的方法不在对象的第一层，这是this只是指向当前一层的对象，而不是继承更上面的层的对象。
```
var a = {
  p: 'Hello',
  b: {
    m: function() {
      console.log(this.p);
    }
  }
};

a.b.m() // undefined
```
a.b.m方法在a对象的第二层，该方法内部的this不是指向a，而是指向a.b。
如果这时将嵌套对象内部的方法赋值给一个变量，this依然会指向全局对象。
## DOM事件处理函数
当函数被用作事件处理函数时，它的this指向触发事件的元素。
```
function bluify(e){
  console.log(this === e.currentTarget); // 总是 true

  console.log(this === e.target);  // 当 currentTarget 和 target 是同一个对象时为 true      
  this.style.backgroundColor = '#A5D9F3';
}

var elements = document.getElementsByTagName('*');

for(var i=0 ; i<elements.length ; i++){
  elements[i].addEventListener('click', bluify, false);
}
```
## 内联事件处理函数
当代码被内联on-event 处理函数调用时，它的this指向监听器所在的DOM元素：
```
<button onclick="alert(this.tagName.toLowerCase());">
  Show this
</button>
```

# 绑定this的方法
this的动态切换，固然为 JavaScript 创造了巨大的灵活性，但也使得编程变得困难和模糊。
有时，需要把this固定下来，避免出现意想不到的情况。
JavaScript 提供了call、apply、bind这三个方法，来切换/固定this的指向。
## .call()
```
var obj = {}

var f = function () {
  return this
}

f() === window // true
f.call(obj) === obj // true
```
全局环境运行函数f时，this指向全局环境（浏览器为window对象）；
call方法可以改变this的指向，指定this指向对象obj，然后在对象obj的作用域中运行函数f。

-------
call方法的参数，应该是一个对象。如果参数为空、null和undefined，则默认传入全局对象。
```
var n = 123;
var obj = { n: 456 };

function a() {
  console.log(this.n);
}

a.call() // 123
a.call(null) // 123
a.call(undefined) // 123
a.call(window) // 123
a.call(obj) // 456
```
call方法还可以接受多个参数.
call的第一个参数就是this所要指向的那个对象，后面的参数则是函数调用时所需的参数。
`func.call(thisValue, arg1, arg2, ...)`
## .apply()
apply方法的作用与call方法类似，也是改变this指向，然后再调用该函数。
唯一的区别就是，它接收一个数组作为函数执行时的参数，使用格式如下。
`func.apply(thisValue, [arg1, arg2, ...])`
利用这一点可以做一些应用，例如找出数组最大元素、将数组的空元素变为undefined、转换类似数组的对象、绑定回调函数的对象。
## .bind()
bind方法用于将函数体内的this绑定到某个对象，然后返回一个新函数。
```
var d = new Date();
d.getTime() // 1481869925657

var print = d.getTime;
print() // Uncaught TypeError: this is not a Date object.
```
getTime内部的方法this绑定Date对象的实例，将d.getTime方法赋给d之后，内部this已经不指向Date实例。
```
var print = d.getTime.bind(d);
print() // 1481869925657
```
bind可以将getTime方法内部的this绑定到d对象，这时就可以安全地将这个方法赋值给其他变量。
