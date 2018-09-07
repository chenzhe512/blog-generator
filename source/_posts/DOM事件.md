---
title: DOM事件
date: 2018-08-14 11:30:03
tags:
---
> DOM事件。
# 如何做操点击别处关闭浮层？
第一阶段：
stopPropagation以为是最终解决方案，如果在button中加一个checkbox，在IE8中会出现bug，点不了checkbox，点击事件不管用。
并且如果页面中存在很多点击方案，那就需要监听多次，浪费内存。
(http://js.jirengu.com/honahuziju/1/edit?html,js,output)
第二阶段：节省内存的方案
如果在checkbox的父元素的任一层添加阻止默认事件，那么就不能check。
`$('#wrapper').on('click',false)`
存在bug，阻止了checkbox。
```
$('#clickMe').on('click',function(){
  $('#popover').show()
  $(document).one('click',function(){
  $('#popover').hide()
})

})

$('#wrapper').on('click',function(e){
  e.preventDefault()
  e.stopPropagation()
})
```
最终是这个，在点击clickMe后再添加document的监听事件，并且是一次的one，如果一直监听的话，只要一点击就监听，会造成内存的浪费。
```
$('#clickMe').on('click',function(){
  $('#popover').show()
  $(document).one('click',function(){
  $('#popover').hide()
})
})
```
这里，在点击一次后，把popover展示出来，并添加一个document监听事件函数，立即执行。所以不会展示浮层。
两种解决方法：
1，阻止事件监听，stopPropagation
2，计时器，一层一层冒泡，通知，完了发现计时器没有执行，就执行，添加fn2，但不会执行，因为通知过程已经完了
，下次点击才会执行。
# 轮播bug
切出去之后过来会出现bug，一下把切出去为播放的页面一次展示出来。
```
document.addEventListener('visibilitychange',function(){
    if(document.hidden){
       window.clearInterval(timer)
    }else{
        timer = setInterval(function(){
            makeLeave(getImage(n))
            .one('transitionend',function(e){
                makeEnter($(e.currentTarget))
            })
            makeCurrent(getImage(n+1))
            n += 1
        },1000)
    }
})
```
## 不一样的轮播-新方案
如果hide后show没有反应，那么你就offset一下。