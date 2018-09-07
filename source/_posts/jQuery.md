---
title: jQuery
date: 2018-08-10 14:15:28
tags:
---
> jQuery,使用最广泛的JavaScript函数库。首先，它是一个DOM操作工具，使得操作DOM对象变得容易；还统一了不同浏览器的API接口，是所有的代码在不同浏览器中都可运行，不必担心差异。

# 实现
如果我想实现一个方法，但DOM和浏览器又没有提供这个API，当进行项目时又会经常使用这个方法，简单的方法就是我把这中方法的代码写出来，放到电脑上建一个函数，当需要使用时，我就把这个函数添加进去再进行调用就行了。
问题：但是每次使用我都得进行添加函数、调用函数这些步骤，显得冗余？
设想另一种方法，在原型与原型链中，知道，浏览器和JS是把这些经常能够实现某种目的的函数的API都是直接存在原型prototype上，用到的时候直接调用很方便。如果我也把自己经常使用的函数存储到DOM或者浏览器的prototype上，我使用的时候直接调用岂不是很方便(怎么没有别人发现这么方便简介的办法？有坑？)
这样就会引起另一个问题（一个问题引起另一个问题bug？）：如果别人已经在prototype上写入了一个函数，那么你又写入了一个函数，那到底谁写的算呀，并不是先入为主，后来的总会覆盖先来的。又或者你写的把浏览器或者DOM的prototype给覆盖掉了（GG），无休止的写下去，岂不是显得（咦，贵圈真乱）？？
[为什么不要直接在Object.prototype上定义方法？(JavaScript):](https://www.zhihu.com/question/26924011)
总结下来就是：做一个项目的时候，你改了一个prototype，你同事也改了一个，最后bug你都不知道从哪找，找到你都感到改bug改的头疼。
退而求其次，那我就目标远大一些，造福一方人嘛，JS和浏览器有它的node接口，我也写一个我自己的接口如何？这个，可能有点难~~~
[设计更好的 JavaScript API：](https://juejin.im/entry/5708de8a7db2a20051cfaf8d)
那么就没有人提前发现这个问题吗，有的【jQuery】。
暂定
# 例
## 实现两个函数getSiblings和addClass
简单写法：` ul>li[id=item$]{选项$}*5 `
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
<ul>
  <li id="item1">选项1</li>
  <li id="item2">选项2</li>
  <li id="item3">选项3</li>
  <li id="item4">选项4</li>
  <li id="item5">选项5</li>
</ul>
</body>
</html>
```
### 获取一个节点的所有兄弟姐妹
```
function getSlibings(node){
  var allChildren = node.parentNode.children;
  var arr = {length:0}
  for (let i = 0; i < allChildren.length; i++) {
    if (allChildren[i] !== node) {
      arr[arr.length] = allChildren[i]  
      arr.length += 1
    }
  } 
  return arr
}
```
重点：arr[arr.length] = allChildren[i] 之所以不用arr[i] = allChildren[i],是应为 arr[i] 是因为可能会跳过，导致 arr 的 key 会不完整；使用 arr[arr.length] 可以很好的给伪数组添加完整的数字 key 。
### 添加删除class
```
function addClass(node,classes){
    for(let key in classes){
        var value = classes[key]
        if(value){
            node.classList.add(key)
        }else{
            node.classList.remove(key)
        }
    }
}
```
## 命名空间
对于以上两个函数可以取一个名字，自己用：
```
window.czdom = {}
czdom.getSlibings = getSlibings
czdom.addClass = addClass
//想用的话只需
czdom.getSlibings(item3)
czdom.getSlibings(item3,{a:xx,b:xx,c:xx})
```
## 也可以
在prototype上添加方法：
```
Node.prototype.getSiblings = function() {
  var allChildren = this.parentNode.children  //使用 this
  var arr = {length:0}
  for (let i = 0; i < allChildren.length; i++) {
    if (allChildren[i] !== this) {
      arr[arr.length] = allChildren[i] 
      arr.length += 1
    }
  } 
  return arr
}

Node.prototype.addClass = function(classes) {
    for (let key in classes) {
    var value = classes[key]
    var methodName = value ? 'add' : 'remove'
    this.classList[methodName](key)
  }
}
```
或者新的接口：
```
window.Node2 = function(node) {
    return {
        getSilings: function() {
          var allChildren = node.parentNode.children 
          var arr = {length:0}
          for (let i = 0; i < allChildren.length; i++) {
            if (allChildren[i] !== node) {
              arr[arr.length] = allChildren[i] 
              arr.length += 1
            }
          } 
          return arr
        },
        addClass: function(classes) {
          for (let key in classes) {
            var value = classes[key]
            var methodName = value ? 'add' : 'remove'
            node.classList[methodName](key)
          }
        }
    }
}
```
后边这种方法就是jquery的思路。即将Node2改为jQuery。
```
window.jQuery = function(nodeOrSelector) {
  let nodes = {}
  if (typeof nodeOrSelector === 'string') {
    let temp = document.querySelectorAll(nodeOrSelector)
    for (let i = 0; i < temp.length; i++) {
      nodes[i] = temp[i]
    }
      nodes.length = temp.length
  }  
  else if (nodeOrSelector instanceof Node) {
    nodes = {0: nodeOrSelector,length: 1}
  }
  
  nodes.getSiblings = function() {}
  nodes.addClass = function(classes) {
    classes.forEach((value) => {
      for (let i = 0; i < nodes.length; i++) {
        nodes[i].classList.add(value)      
      }      
    }) 
  }
  nodes.text = function (text) {
    if (text === undefined) {
      let texts = []
      for (let i = 0; i < nodes.length; i++) {
        texts.push(nodes[i].textContent)
      }
      return texts
    }
    else {
      for (let i = 0; i < nodes.length; i++) {
        nodes[i].textContent = text
      }
      return texts
    }
  }
  return nodes
}
```