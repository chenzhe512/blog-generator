---
title: HTML标签
date: 2018-06-01 16:52:51
tags:
-
# HTML标签
## `<iframe>标签`
HTML内联框架元素iframe表示嵌套的浏览上下文，有效的将另一个HTML页面嵌入到当前页面中。   
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
  iframe{
   width:100%;
   height:400px;
  }
  </style>
</head>
<body>
<iframe name=xxx src="#" frameborder="0"></iframe>
  <a target=xxx href="http://qq.com">QQ</a>
  <a target=xxx href="https://baidu.com">百度</a>
</body>
</html>
```
1. iframe新打开的窗口中默认为有边框，可以使用`frameborder="0"`来取消边框；
2. iframe默认高度为100*50，可以通过CSS来指定frame的宽度和高度（宽度可以用百分比，高度不能用）；
3. 与`<a>`元素配合使用，`src="#"`表示当前页面，`name=xxx`和`target=xxx`中的name和target对应，类似于iframe建立一个空白的窗口供当前页面调用，命名为xxx，a标签可以通过target来调用这个新的窗口，显示的内容由herf决定；(src支持相对路径和绝对路径)
## `<a>`标签(发起GET请求)
HTML中的a元素/锚元素（auchor)可以创建一个到其他网页、文件、同一页面内位置、电子邮件或其他任何URL的超链接。
### href属性
这是一个必须属性，为锚（`<a>`）定义一个超文本链接来源。表示链接目标的URL（外部链接）或URL片段（内部链接）。URL片段是由一个hash符号（#），它指定一个内部目标在当前文档中的位置（ID）开头的名字。URL不限于HTTP协议，可以使用浏览器所支持的任何协议，如FTP等。
eg：
1. 链接外部地址
`<a herf="http://www.baidu.com/">百度</a>`
2. 链接到本页的某个部分
`<a href="#属性">相同页面链接</a>`
3. 创建一个可点击的图片
```<a href="https://developer.mozilla.org/en-US/">
  <img src="https://mdn.mozillademos.org/files/6851/mdn_logo.png" 
       alt="MDN logo" />
</a>
```
4. 创建一个Email链接 
`<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>`
5. 创建电话链接
`<a href="tel:+491570156">+49 157 0156</a>`
易错示例：
`<a href="//qq.com">QQ</a>`
这是a标签的无协议绝对地址，会继承当前页面的协议（如当前为HTTP协议，即继承HTTP）
`<a href="xxx.html">QQ</a>`
如果此时处于index.html页面，点击之后所处的页面是/xxx.html，而不是/index.heml/xxx.html,在写这个路径的时候是只以目录为参考的，与文件无关。
`<a href="#sssss">sssss</a>`
此时点击之后是处于/index.html#sssss，不发送请求，应为锚点是不发送请求的，是页面内的跳转，其他都发送请求。
`<a href="?name=frank">frank</a>`
此时点击是处于/index.html?name=frank,并发送一个GET请求。
`<a href="javascript: ;">QQ</a>
这是a标签的伪协议，点击之后什么也不做的链接。
`<a href="#">qq</a>
标签点击之后页面会刷新。
`<a href="">qq</a>
会刷新页面，发送请求。

### target属性
该属性指定在何处显示链接的资源，例如是在本窗口直接打开还是新开窗口？
`<a href="http://..." target="_black">xxx</a>
target属性一共有四中属性：
1. _self:当前页面加载，即当前响应到当前页面上。（默认属性）
2. _blank:新窗口打开，即到一个新的未命名的浏览器窗口上打开。
3. _parent:加载响应到当前框架的HTML4父框架或HTML5浏览上下文的父浏览上打开。（简单理解为到当前页面的上一个页面打开）
4. _top:加载响应在进入顶层浏览上加载。
### download属性
download属性指示浏览器下载URL而不是导航加载到URL,因此将提示用户将其保存为本地文件。
`<a href="http://..." download>下载</a>
1. HTTP响应的`Content-type: application/octet-stream`,那么浏览器会以下载的形式接受这个请求而不是在页面展示。
2. 或是在a标签上写download也会下载.
## `<form>`标签(发起POST请求)
HTML中form元素表示了文档中的一个区域，这个区域包含交互控制元件，用于向web服务器提交信息。
```
<form action="users" method="post">
  <input type="text" name="xxx">
  <input type="psssword" name="yyy">
  <input type="submit" value="提交">
</form>
```
1. 如果form标签没有提交按钮，就无法提交，除非用JS.
2. form标签主要发起一个POST请求，至于POST请求响应什么，form不管。
3. form标签中的name最终会被代入请求中的第四部分最为它的key。
`<form action="users" methdo="get/post">`这段中，如果是GET会默认把输入的内容参数放入查询参数中，而POST会把参数放入请求的第四部分，可以通过给URL直接加参数来实现让POST也有查询参数（`form action="users?zzz=3" method="post">`)，但不能通过任何方法让GET有第四部分。
### form标签的target属性
与a标签类似。
## input/button标签
### button标签
`<button>HI</button>`
button如果没有写type，会自动升级为提交（submit)按钮。
`<button type="button">HI</button>`
button如果写了type="button",那么就没有提交（submit）按钮。
### input
`<input type="button" value="hi">
这个表单不能提交，这只是一个普通按钮。
`<input tupe="submit" value="hi">
这个表单可以提交，submit是唯一可以确定这个form表单可以提交的。
## checkbox/radio属性
### checkbox
checkbox是复选框，如果单独出现没有意义，因为你不确定点这个框是为了选择什么，所以一般在右边/左边写一些文字选择。如果想要实现点击文字就可以选择的情况，那就需要用labal标签将其包起来。
eg：
`<input type="checkbox" id="xxx"><label for="xxx">是否</label>`
`<label for="xxx">用户名</label><input type="text" name="xxx" id="xxx">
其中label for="xxx"，和input的id="xxx"是关联的一对，需要一起出现。
简便的写法：
`<label><input type="checkbox">是否</label>`
`<label>用户名<input type="text" name="xxx"></label>`
直接用label把input包起来，不需要写for="xxx"和id="xxx"
### radio
提交表单都需要给一个name，不然服务器是接收不到的。即上文的xxx改成有意义的。
```
<label>用户名<input type="text" name="username"></label>
<label>密码<input type="password" name="password"></label>
最喜欢的水果
<label><input type="checkbox" name="fruit" value="orange">橘子</label>
<label><input type="checkbox" name="fruit" value="banana">香蕉</label>
爱我
<label><input type="radio" name="loveme" value="yes">Yes</label>
<label><input type="radio" name="loveme" value="No">No</label>
```
如果单选框radio的选择有同一个name的，那么只有一个会被选中；
上面对比可以看出单选框和复选框除了type属性不同外，name分别都相同，checkbox确定了可以多项选择，radio确定了多个选项只能选择一个。radio中name一个作用是如果name相同只有一个被选中，另一个作用是告诉服务器你是什么name。
## select
```
<select name="group" multiple>
  <option value="">-</option>
  <option value="1">第一组</option>
  <option value="2">第二组</option>
  <option value="3" disabled>第三组</option>
  <option value="1" selected>第四组</option>
</select>
```
其中value=""代表什么都不选，disabled代表无法选，selected代表默认选择,multiple代表多选（按着shift）
```
<textarea style="resize:none;weight=200px;height=200px;" name="爱好"  ></textarea>
<textarea  name="爱好" id="" cols="30" rows="10"></textarea>
```
第一种使用CSS来精确大小，第二种是粗略。
## table
```
<table border=1>
  <colgroup>
    <col width=100></col>  
    <col bgcolor=red width=200></col>
    <col width=100></col>
    <col width=70></col>
  </colgroup>
  <thead>
    <tr>
      <th>项目</th><th>姓名</th><th>班级</th><th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th></th><td>小明</td><td>1</td><td>94</td>
    </tr>
    <tr>
      <th></th><td>小红</td><td>2</td><td>96</td>
    </tr>
    <tr>
      <th>平均分</th><td></td><td></td><td>95</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th>总分</th><td></td><td></td><td>190</td>
    </tr>
  </tfoot>
</table>
```
一个完整的表格。注：table 的 border 默认是占据空间的，可以使用 css 属性 border-collapse: collapse 来合并边框