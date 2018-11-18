---
title: AJAX
date: 2018-08-22 09:33:43
tags:
---
> AJAX---异步的JavaScript与XML技术
![4-min.jpg](https://i.loli.net/2018/08/22/5b7d3911bdf47.jpg)


<!--more-->
# 1.简介
维基百科
AJAX即“Asynchronous JavaScript and XML”（异步的JavaScript与XML技术），指的是一套综合了多项技术的浏览器端网页开发技术。Ajax的概念由杰西·詹姆士·贾瑞特所提出。
传统的Web应用允许用户端填写表单（form），当提交表单时就向网页服务器发送一个请求。服务器接收并处理传来的表单，然后送回一个新的网页，但这个做法浪费了许多带宽，因为在前后两个页面中的大部分HTML码往往是相同的。由于每次应用的沟通都需要向服务器发送请求，应用的回应时间依赖于服务器的回应时间。这导致了用户界面的回应比本机应用慢得多。
与此不同，AJAX应用可以仅向服务器发送并取回必须的数据，并在客户端采用JavaScript处理来自服务器的回应。因为在服务器和浏览器之间交换的数据大量减少，服务器回应更快了。同时，很多的处理工作可以在发出请求的客户端机器上完成，因此Web服务器的负荷也减少了。
类似于DHTML或LAMP，AJAX不是指一种单一的技术，而是有机地利用了一系列相关的技术。虽然其名称包含XML，但实际上数据格式可以由JSON代替，进一步减少数据量，形成所谓的AJAJ。而客户端与服务器也并不需要异步。一些基于AJAX的“派生／合成”式（derivative/composite）的技术也正在出现，如AFLAX。
# 2.演变
# 2.1 如何发送请求？
最初的具有局限性的发送请求的几种方式：
*    用 form 可以发请求，但是会刷新页面或新开页面
*    用 a 可以发 get 请求，但是也会刷新页面或新开页面
*    用 img 可以发 get 请求，但是只能以图片的形式展示
*    用 link 可以发 get 请求，但是只能以 CSS、favicon 的形式展示
*    用 script 可以发 get 请求，但是只能以脚本的形式运行
局限性在于刷新页面，占用内存资源，带宽浪费，如果我想事项以下两个条件：
1. get、post、put、delete 请求都行
2. 形式不定，即想以什么形式展示就以什么形式展示
# 2.2新突破
IE 5 率先在 JS 中引入 ActiveX 对象（API），使得 JS 可以直接发起 HTTP 请求。
随后 Mozilla、 Safari、 Opera 也跟进（抄袭）了，取名 XMLHttpRequest，并被纳入 W3C 规范。
# 2.3规范化
Jesse James Garrett将这个技术取名为AJAX：异步的JavaScript和XML。
1. 创建 AJAX 对象, 即 XMLHttpRequest
2. 使用XMLHttpRequest发请求
3. 服务器返回XML格式的字符串，只能返回字符串
4. JS解析XML，并更新局部页面
# 示例
## 原生JS写一个AJAX请求
```
let request = new XMLHttpRequest(); 
request.open('GET','/xxx'); 
request.send();
request.onreadystatechange = ()=>{
  if(request.readyState === 4){
    if(request.status >= 200 && request.status < 300){
      var string = request.responseText;
      var value = JSON.parse(string);
    }
  }
}
```
* let request = new XMLHttpRequest() 创建一个AJAX实例

* request.open(method,address) 初始化请求，一般有3个参数 ，如果没有设置就是 默认值
request.open(method,url,async)
method ：请求的类型；GET 或 POST
url ： 文件在服务器上的位置
async ：true（异步）或 false（同步）

* request.send() 发送请求(如果参数为String，只能为 post请求)

* reqeust.onreadystatechange() 监听 readystatue 的变化 ，每当 readyState 改变时，就会触发 onreadystatechange 事件。

* request.readyState XMLHttpRequest 的状态。从 0 到 4 发生变化
| 0 | UNSENT(未打开) | open()方法还未被调用，请求未初始化 |
| 1 | OPENED (未发送) | open()方法已经被调用， 服务器连接已建立 |
| 2 | HEADERS_RECEIVED (已获取响应头) | send()方法已经被调用, 响应头和响应状态已经返回.请求已接收 |
| 3 | LOADING (正在下载响应体) | 响应体下载中; responseText中已经获取了部分数据. |
| 4 | DONE (请求完成) | 整个请求过程已经完毕. |
# 同源策略
* form、img、script等上面提到的请求方式，是可以对别的域名发送请求的。
但用AJAX不能对别的域名放送请求，只有协议、域名、端口号一摸一样才允许发送AJAX（多个www是不同的域名）
因为AJAX是可以获取响应内容的，如果没有同源策略的限制，别的网站可以通过AJAX获取另一个网站的所有信息。
* AJAX可以通过CORS发送请求到别的网站
跨域资源共享：Cross-Origin Resource Sharing
在需要访问的服务器里添加一句
```
response.setHeader('Access-Control-Allow-Origin', '*')
```

# AJAX问题
## 1.封装一个 jQuery.ajax
```
window.jQuery = function(nodeOrSelector){
  let nodes = {}
  nodes.addClass = function(){}
  nodes.html = function(){}
  return nodes
}
window.$ = window.jQuery

window.jQuery.ajax = function({url, method, body, successFn, failFn, headers}){
  let request = new XMLHttpRequest()
  request.open(method, url) // 配置request
  for(let key in headers) {
    let value = headers[key]
    request.setRequestHeader(key, value)
  }
  request.onreadystatechange = ()=>{
    if(request.readyState === 4){
      if(request.status >= 200 && request.status < 300){
        successFn.call(undefined, request.responseText)
      }else if(request.status >= 400){
        failFn.call(undefined, request)
      }
    }
  }
  request.send(body)
}

function f1(responseText){}
function f2(responseText){}

myButton.addEventListener('click', (e)=>{
  window.jQuery.ajax({
    url: '/frank',
    method: 'get',
    headers: {
      'content-type':'application/x-www-form-urlencoded',
      'frank': '18'
    },
    successFn: (x)=>{
      f1.call(undefined,x)
      f2.call(undefined,x)
    },
    failFn: (x)=>{
      console.log(x)
      console.log(x.status)
      console.log(x.responseText)
    }
  })
})
```
## 2.升级jQuery.ajax 满足 Promise 规则
```
window.jQuery = function(nodeOrSelector){
  let nodes = {}
  nodes.addClass = function(){}
  nodes.html = function(){}
  return nodes
}
window.$ = window.jQuery

window.Promise = function(fn){
  // ...
  return {
    then: function(){}
  }
}

window.jQuery.ajax = function({url, method, body, headers}){
  return new Promise(function(resolve, reject){
    let request = new XMLHttpRequest()
    request.open(method, url) // 配置request
    for(let key in headers) {
      let value = headers[key]
      request.setRequestHeader(key, value)
    }
    request.onreadystatechange = ()=>{
      if(request.readyState === 4){
        if(request.status >= 200 && request.status < 300){
          resolve.call(undefined, request.responseText)
        }else if(request.status >= 400){
          reject.call(undefined, request)
        }
      }
    }
    request.send(body)
  })
}

myButton.addEventListener('click', (e)=>{
  let promise = window.jQuery.ajax({
    url: '/xxx',
    method: 'get',
    headers: {
      'content-type':'application/x-www-form-urlencoded',
      'frank': '18'
    }
  })
  promise.then(
    (text)=>{console.log(text)},
    (request)=>{console.log(request)}
  )
})
```

