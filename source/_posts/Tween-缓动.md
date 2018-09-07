---
title: Tween-缓动
date: 2018-07-26 21:18:22
tags:
---
>Tween,好用的缓动工具。
# Tween
Google搜索Tween或者直接进入github.com/tweenjs/tween.js。看到示例：
```
var box = document.createElement('div');
box.style.setProperty('background-color', '#008800');
box.style.setProperty('width', '100px');
box.style.setProperty('height', '100px');
document.body.appendChild(box);

// Setup the animation loop. 设置动画循环
function animate(time) {
    requestAnimationFrame(animate);
    TWEEN.update(time);
}
requestAnimationFrame(animate);

var coords = { x: 0, y: 0 }; // Start at (0, 0) 从0,0开始
var tween = new TWEEN.Tween(coords) // Create a new tween that modifies 'coords'. 创建一个修改“coords”的新补间。
        .to({ x: 300, y: 200 }, 1000) // Move to (300, 200) in 1 second. 在1秒内移动到（300,200）。
        .easing(TWEEN.Easing.Quadratic.Out) // Use an easing function to make the animation smooth. 使用缓动功能使动画流畅。
        .onUpdate(function() { // Called after tween.js updates 'coords'. 在tween.js更新'coords'之后调用。
            // Move 'box' to the position described by 'coords' with a CSS translation. 使用CSS翻译将'box'移动到'coords'描述的位置。
            box.style.setProperty('transform', 'translate(' + coords.x + 'px, ' + coords.y + 'px)');
        })
        .start(); // Start the tween immediately. 立即启动补间。
```
```
Installation(安装)
Download the library and include it in your code:

<script src="js/Tween.js"></script>
You can also reference a CDN-hosted version in your code, thanks to cdnjs. For example:
（您还可以在代码中引用CDN托管版本，这要归功于cdnjs。例如：）
<script src="https://cdnjs.cloudflare.com/ajax/libs/tween.js/16.3.5/Tween.min.js"></script>
See tween.js for more versions.
```
实际使用就是Google搜索CDNJS，进入后搜索Tween，这即是通过引用CDN库来进行使用。使用范例：
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/tween.js/17.2.0/Tween.min.js"></script>
<script>
function animate(time) {
    requestAnimationFrame(animate);
    TWEEN.update(time);
}
requestAnimationFrame(animate);

let currentTop = window.scrollY
let targetTop = top - 80
let s = targetTop - currentTop
var coords = {y: currentTop}; 
var t = Math.abs((s/100)*300)
if(t>500){
	t = 500
}
var tween = new TWEEN.Tween(coords) 
.to({y: targetTop }, t) 
.easing(TWEEN.Easing.Quadratic.In) 
.onUpdate(function() { 
	window.scrollTo(0,coords.y)
})
.start(); 
```
# 新的API和CSS属性
## @keyframes和animation
@keyframes 规则通过在动画序列中定义关键帧（或waypoints）的样式来控制CSS动画序列中的中间步骤。这比转换(transition)更能控制动画序列的中间步骤。
@keyframes:
```
@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}
```
要使用关键帧, 先创建一个带名称的@keyframes规则，以便后续使用 animation-name 这个属性来将一个动画同其关键帧声明匹配。
每个@keyframes 规则包含多个关键帧，也就是一段样式块语句，每个关键帧有一个百分比值作为名称，代表在动画进行中，在哪个阶段触发这个帧所包含的样式。
您可以按任意顺序列出关键帧百分比；他们将按照其应该发生的顺序来处理。
1. 如果一个关键帧规则没有指定动画的开始或结束状态（也就是，0%/from 和100%/to，浏览器将使用元素的现有样式作为起始/结束状态。
2. 如果多个关键帧使用同一个名称，以最后一次定义的为准。
3. 如果一个关键帧中没有出现其他关键帧中的属性，那么这个属性将使用插值(不能使用插值的属性除外, 这些属性会被忽略掉)。
4. 关键帧中出现的 !important 关键词将会被忽略,示例：
```
@keyframes important1 {
  from { margin-top: 50px; }
  50%  { margin-top: 150px !important; } /* 忽略 */
  to   { margin-top: 100px; }
}
```