---
title: CSS学习之Selectors、animation等
date: 2018-07-27 15:13:08
tags:
---
> 本文主要是对于学习中遇到的新CSS属性知识的总结，包括选择器(Selectors)、动画(Animation)、光标(Cursor)、z-index，以便加深记忆了解。
# Selectors
CSS选择器规定了CSS规则会应用到哪些元素上。
## 基本选择器
### 类型（Type）选择器
这种基本选择器会匹配 **所有给定元素名** 的元素。也叫做标签/元素选择器，匹配 **所有使用某个标签** 的元素。
**语法：元素{样式声明}**
```
div{
  width: 200px;
  height: 200px;
  background: #000;
  border: 1px solid red;
}
```
如上，所有的div都会应用以上的CSS属性。
### 类（Class）选择器
这种选择器会基于 **类属性的值** 来选择元素。
**语法：.classname{样式声明}**/ 等价于 **[class~=类名] {样式声明 }**
```
.ruguo{
  background: #000;
  border: 10px solid red;
}
```
如上，所有的class="ruguo"的元素（标签）都会应用.ruguo的CSS属性。
如果是div.ruguo{},则会应用与以下：
```
<div class="ruguo"></div>
```
即应用于class="ruguo"的div标签。
### ID选择器
这种选择器会选择 **所有id属性与之匹配** 的元素。注：一个文档中的每一个id都应该是唯一的。
**语法：#idname**/等价于[id=id属性] {样式声明 }
```
#liebiao{
    font-size: 20px;
}
```
如上，所有的id="liebiao"的元素（标签）都会应用#liebiao的CSS属性。
### 通用选择器
这个选择器会选择所有的节点。通常与一个名词空间配合使用，选择这个空间下的所有元素。
语法：*
```
*{
  margin: 0;
  padding: 0;
}
```
页面内所有元素都会运用*的属性。
### 属性选择器
这个基本的选择器根据元素的属性来进行选择。
语法：
1. E[att]：匹配所有具有att属性的E元素，不考虑它的值。例如resume中的[data-x]
2. E[att=val]：匹配所有att属性等于"val"的E元素。
3. E[att~=val]：匹配所有att属性具有多个空格分隔的值、其中一个值等于"val"的E元素。
4. E[att|=val]：匹配所有att属性具有多个连字号分隔（hyphen-separated）的值、其中一个值以"val"开头的E元素，主要用于lang属性，比如"en"、"en-us"、"en-gb"等等
```
p[title] { color:#f00; }
div[class=error] { color:#f00; }
td[headers~=col1] { color:#f00; }
p[lang|=en] { color:#f00; }
blockquote[class=quote][cite] { color:#f00; }
```
## 多元素的组合选择器
### 相邻选择器
它只会匹配紧跟其前方元素的同胞（同级）元素.
语法：前方元素 + 目标元素 {样式声明 }
例如：
```
<ul>
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
</ul>
hr
li + li {
  color: red;
}
```
用一个结合符只能选择两个相邻兄弟中的第二个元素。
上面这个选择器只会把列表中的第二个和第三个列表项变为红色。第一个列表项不受影响。
### 通用兄弟选择器
在使用 ~ 连接两个元素时,它会匹配第二个元素,条件是它必须跟(不一定是紧跟)在第一个元素之后,且他们都有一个共同的父元素 。
语法：元素 ~ 元素 {样式声明 }
```
<span>This is not red.</span>
<p>Here is a paragraph.</p>
<code>Here is some code.</code>
<span>And here is a span.</span>
hr
p ~ span {
  color: red;
}
```
这个CSS属性只会让第二个span中的字体变为红色，其他不受影响。
### 子选择器
当使用  > 选择符分隔两个元素时,它只会匹配那些作为第一个元素的直接后代(子元素)的第二元素. 与之相比, 当两个元素由 后代选择器 相连时, 它表示匹配存在的所有由第一个元素作为祖先元素(但不一定是父元素)的第二个元素, 无论它在 DOM 中"跳跃" 多少次。
语法：元素1 > 元素2 {样式声明 }
```
<div>
  <span>Span 1. In the div.
    <span>Span 2. In the span that's in the div.</span>
  </span>
</div>
<span>Span 3. Not in a div at all</span>
hr
span { background-color: white; }
div > span {
  background-color: DodgerBlue;
}
```
如上，div > span中的属性只会让span1中的字体变为DodgerBlue，span2和span3不受影响。
### 后代选择器
当使用 ␣ 选择符 (这里代表一个空格,更确切的说是一个或多个的空白字符) 连接两个元素时使得该选择器可以只匹配那些由第一个元素作为祖先元素的所有第二个元素(后代元素) . 后代选择器与 子选择器 很相似, 但是后代选择器不需要相匹配元素之间要有严格的父子关系.
语法：元素1 元素2 {样式声明 }
```
<div>
  <span>Span 1.
    <span>Span 2.</span>
  </span>
</div>
<span>Span 3.</span>
hr
span { background-color: white; }
div span { background-color: DodgerBlue; }
```
以上只要是span的后代元素都会应用div span的CSS样式。即span1和span2，span3为div的同级元素，一辈儿的。
### 多元素选择器
多元素选择器，同时匹配所有E元素或F元素，E和F之间用逗号分隔
语法：元素1,元素2{样式声明}
元素1和元素2都匹配CSS样式。
## 伪类及伪元素选择器
### 伪类
### 伪元素
1. ::before
CSS中，::before 创建一个伪元素，其将成为匹配选中的元素的第一个子元素。常通过 content 属性来为一个元素添加修饰性的内容。此元素默认为行内元素。(在一个元素之前插入生成的内容)
例如：
```
a::before {
  content: "♥";
}
```
2. ::after
CSS伪元素::after用来创建一个伪元素，做为已选中元素的最后一个子元素。通常会配合content属性来为该元素添加装饰内容。这个虚拟元素默认是行内元素。(在一个元素之后插入生成的内容)
3. ::first-line
::first-line CSS pseudo-element （CSS伪元素）在某 block-level element （块级元素）的第一行应用样式。第一行的长度取决于很多因素，包括元素宽度，文档宽度和文本的文字大小。(匹配一个元素的第一行)
4. ::first-letter
CSS 伪元素 ::first-letter会选中某 block-level element（块级元素）第一行的第一个字母，并且文字所处的行之前没有其他内容如图片和内联的表格。(匹配一个元素的第一个字母)
其他伪元素(https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-elements)
### 伪类
1. :first-child 
:first-child CSS伪类 代表了一组兄弟元素中的第一个元素。（匹配父元素的第一个子元素）
2. :link
:link伪类选择器是用来选中元素当中的链接。它将会选中所有尚未访问的链接，包括那些已经给定了其他伪类选择器的链接（例如:hover选择器，:active选择器，:visited选择器）。为了可以正确地渲染链接元素的样式，:link伪类选择器应当放在其他伪类选择器的前面，并且遵循LVHA的先后顺序，即：:link — :visited — :hover — :active。:focus伪类选择器常伴随在:hover伪类选择器左右，需要根据你想要实现的效果确定它们的顺序。
3. :visited	
匹配所有已被点击的链接
4. :active
匹配鼠标已经其上按下、还没有释放的E元素
5. :hover
匹配鼠标悬停其上的E元素
6. :focus
匹配获得当前焦点的E元素
7. :lang(c)	
匹配lang属性等于c的E元素
其他伪类:(https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)
阮一峰相关资料:(http://www.ruanyifeng.com/blog/2009/03/css_selectors.html)
hr
# Animation
CSS animations 使得可以将从一个CSS样式配置转换到另一个CSS样式配置。动画包括两个部分:描述动画的样式规则(animation)和用于指定动画开始、结束以及中间点样式的关键帧(@keyframes)。
## Animation属性
1. animation-delay
设置延时，即从元素加载完成之后到动画序列开始执行的这段时间。
值：从动画样式应用到元素上到元素开始执行动画的时间差。该值可用单位为秒(s)和毫秒(ms)。如果未设置单位，定义无效。
2. animation-direction
设置动画在每次运行完后是反向运行还是重新回到开始位置重复运行。
3. animation-duration
设置动画一个周期的时长。
4. animation-iteration-count
设置动画重复次数， 可以指定infinite无限次重复动画
5. animation-name
指定由@keyframes描述的关键帧名称。
6. animation-play-state
允许暂停和恢复动画。
7. animation-timing-function
设置动画速度， 即通过建立加速度曲线，设置动画在关键帧之间是如何变化。
8. animation-fill-mode
指定动画执行前后如何为目标元素应用样式。
详细信息：(https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
hr
animation也是一个简写形式。
```
div:hover {
  animation: 1s 1s rainbow linear 3 forwards normal;
}
```
这是一个简写形式，可以分解成各个单独的属性.
```
div:hover {
  animation-name: rainbow;
  animation-duration: 1s;
  animation-timing-function: linear;
  animation-delay: 1s;
  animation-fill-mode:forwards;
  animation-direction: normal;
  animation-iteration-count: 3;
}
```
## @keyframes
keyframes关键字用来定义动画的各个状态，它的写法相当自由。
```
@keyframes rainbow {
  0% { background: #c00 }
  50% { background: orange }
  100% { background: yellowgreen }
}
```
0%可以用from代表，100%可以用to代表.
阮一峰相关资料：(http://www.ruanyifeng.com/blog/2014/02/css_transition_and_animation.html)
# Cursor
Cursor属性定义鼠标指针悬浮在元素上方显示的鼠标光标。
取值：pointer、progress、wait等。
详细：(https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor)
# z-index
z-index 属性指定了一个具有定位属性的元素及其子代元素的 z-order。 当元素之间重叠的时候，z-order 决定哪一个元素覆盖在其余元素的上方显示。 通常来说 z-index 较大的元素会覆盖较小的一个。
对于一个已经定位的元素（即position属性值是非static的元素），z-index 属性指定：
元素在当前堆叠上下文中的堆叠层级。
元素是否创建一个新的本地堆叠上下文。
## 取值
auto
元素不会建立一个新的本地堆叠上下文。当前堆叠上下文中新生成的元素和父元素堆叠层级相同。
<integer>
整型数字是生成的元素在当前堆叠上下文中的堆叠层级。元素同时会创建一个堆叠层级为0的本地堆叠上下文。这意味着子元素的 z-indexes 不与元素外的其余元素的 z-indexes 进行对比。







