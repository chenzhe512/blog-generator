---
title: HTTP
date: 2018-05-28 14:41:34
tags:
---
# 概念
## URI
URI(Uniform Resource Identifier),即统一资源标识符，是一个用于标识某一互联网资源名称的字符串。该种标识允许用户对网络中(www)的资源通过特定的协议进行交互操作。
URI最常见的形式为URL(统一资源定位符,Uniform Resource Locator)，和罕见的用法URN(统一资源名称,Uniform Resource Name):
![URL](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/url.png)
URL包括协议、域名、端口号、路径、查询参数、锚点。图中没有端口
URL如图通过URL你可以确定一个唯一的网址。https://www.baidu.com/s?wd=hello&rsv_spt=1#5，其中.com是顶级域名，baidu是二级域名，www是三级域名。
URN,ISBN: 9787115275790 就是一个 URN，通过 URN 你可以确定一个「唯一的」资源，ISBN: 9787115275790 对应的资源的是《JavaScript 高级程序设计（第三版）》这本书。你去是介绍任何一个图书馆、书店，他们都知道是这本书。
URI可被视为定位符（URL），名称（URN）或两者兼备。统一资源名（URN）如同一个人的名称，而统一资源定位符（URL）代表一个人的住址。换言之，URN定义某事物的身份，而URL提供查找该事物的方法。
## HTTP
HTTP(超文本传输协议，HyperText Transfer Protocol)，一种用于分布式、协作式和超媒体信息系统的应用层协议。HTTP是万维网的数据通信的基础。
设计HTTP最初的目的是为了提供一种发布和接收HTML页面的方法。通过HTTP或者HTTPS协议请求的资源由统一资源标识符（Uniform Resource Identifiers，URI）来标识。
## HTML
HTML(超文本标记语言,HyperText Markup Language）是一种用于创建网页的标准标记语言。HTML是一种基础技术，常与CSS、JavaScript一起被众多网站用于设计令人赏心悦目的网页、网页应用程序以及移动应用程序的用户界面[1]。网页浏览器可以读取HTML文件，并将其渲染成可视化网页。HTML描述了一个网站的结构语义随着线索的呈现，使之成为一种标记语言而非编程语言。
## DNS
DNS(域名系统,Domain Name System）是互联网的一项服务。它作为将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。DNS使用TCP和UDP端口53。当前，对于每一级域名长度的限制是63个字符，域名总长度则不能超过253个字符。
DNS的作用是输入域名，输出对应的IP。
# 请求与响应
## 请求
### 请求的格式
1 动词 路径 协议/版本
2   Key1: value1
    Key2: value2
    Key3: value3
    Content-Type: application/x-www-form-urlencoded
    Host: www.baidu.com
    User-Agent: curl/7.54.0
3 
4 要上传的数据
### 补充
1.请求最多四部分，最少三部分，第四部分可以为空
2.第三部分永远为一个回车
3.动词包括GET,POST,PUT,PATCH,DELETE,HEAD,OPTIONS等；GET为获取信息，POST为上传信息，PUT为整体更新，PATCH为局部更新，DELETE为删除
4.路径包括查询参数但不包括锚点
5.如果没写路径，默认为/
6.第二部分中的Content-Type标注了第四部分的格式
例如：
```
> POST / HTTP/1.1
> Host: www.baidu.com
> User-Agent: curl/7.55.0
> Accept: */*
> Frank: xxx
> Content-Length: 10
> Content-Type: application/x-www-form-urlencoded
>
} [10 bytes data]
```
## 响应
### 响应的格式
1 协议/版本号 状态码 状态解释
2   Key1: value1
    Key2: value2
    Content-Length: 17931
    Content-Type: text/html
3
4 要下载的内容
### 补充
#### 1xx消息
这一类型的状态码，代表请求已被接受，需要继续处理。这类响应是临时响应，只包含状态行和某些可选的响应头信息，并以空行结束。由于HTTP/1.0协议中没有定义任何1xx状态码，所以除非在某些试验条件下，服务器禁止向此类客户端发送1xx响应。[4] 这些状态码代表的响应都是信息性的，标示客户应该采取的其他行动。
#### 2xx成功
这一类型的状态码，代表请求已成功被服务器接收、理解、并接受。
其中200已接受请求，但尚未处理（GET），204服务器成功处理了请求，没有返回任何内容（POST)
#### 3xx重定向
这类状态码代表需要客户端采取进一步的操作才能完成请求。通常，这些状态码用来重定向，后续的请求地址（重定向目标）在本次响应的Location域中指明。
当且仅当后续的请求所使用的方法是GET或者HEAD时，用户浏览器才可以在没有用户介入的情况下自动提交所需要的后续请求。客户端应当自动监测无限循环重定向（例如：A→B→C→……→A或A→A），因为这会导致服务器和客户端大量不必要的资源消耗。按照HTTP/1.0版规范的建议，浏览器不应自动访问超过5次的重定向。
301被请求的资源已**永久移动到新位置**，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。如果可能，拥有链接编辑功能的客户端应当自动把请求的地址修改为从服务器反馈回来的地址。除非额外指定，否则这个响应也是可缓存的。
302要求客户端执行**临时重定向**。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在Cache-Control或Expires中进行了指定的情况下，这个响应才是可缓存的。
304表示**资源未被修改**，因为请求头指定的版本If-Modified-Since或If-None-Match。在这种情况下，由于客户端仍然具有以前下载的副本，因此不需要重新传输资源。
#### 4xx客户端错误
这类的状态码代表了客户端看起来可能发生了错误，妨碍了服务器的处理。除非响应的是一个HEAD请求，否则服务器就应该返回一个解释当前错误状况的实体，以及这是临时的还是永久性的状况。这些状态码适用于任何请求方法。浏览器应当向用户显示任何包含在此类错误响应中的实体内容。
#### 5xx服务器错误
表示**服务器无法完成明显有效的请求**。这类状态码代表了服务器在处理请求的过程中有错误或者异常状态发生，也有可能是服务器意识到以当前的软硬件资源无法完成对请求的处理。除非这是一个HEAD请求，否则服务器应当包含一个解释当前错误状态以及这个状况是临时的还是永久的解释信息实体。浏览器应当向用户展示任何在当前响应中被包含的实体。这些状态码适用于任何响应方法。
例如：
```
< HTTP/1.1 302 Found
< Connection: Keep-Alive
< Content-Length: 17931
< Content-Type: text/html
< Date: Mon, 28 May 2018 07:54:08 GMT
< Etag: "54d97485-460b"
< Server: bfe/1.0.8.18
<
{ [1440 bytes data]
```
# 用Chrome查看HTTP请求与响应内容
首先，右键单击Chrome页面空白处弹出对话框的检查按钮
![检查](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/%E6%A3%80%E6%9F%A5.jpg)
选择页面的Network选项
![Network](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/Network.jpg)
在页面上刷新一下就会向服务器发送一个请求同时会接受一个响应，单击类型为document的文件
![Doc](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/Doc.jpg)
右侧会出现如下图的三个选项，Response为响应，Request为请求,由此就得到了刷新一个页面这个操作的HTTP请求和响应内容
![内容](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/%E5%86%85%E5%AE%B9.jpg)
## 请求内容
点开Request Headers选项后，一定要点下**view source**，得到如下:
```
GET /courses/ec3a5e28-02da-47d6-9226-927db23e82a2 HTTP/1.1
Host: xiedaimala.com
Connection: keep-alive
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: UM_distinctid=1638743d0ca79-082af185a2f84e-3c3c520d-100200-1638743d0cb18a; CNZZDATA1271340636=996656435-1526978113-https%253A%252F%252Fxiedaimala.com%252F%7C1527498
```
## 响应内容
点开Response Headers选项，也一定要点下**view source**，如下：
```
HTTP/1.1 200 OK
Server: nginx/1.4.6 (Ubuntu)
Date: Mon, 28 May 2018 09:56:56 GMT
Content-Type: text/html; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
Cache-Control: max-age=0, private, must-revalidate
Set-Cookie: _task_center_session=YjFtRUYvQzVOcHl1SDlueXhlQ1hRbDNKUUh1alg0VE9ZbHlNdzVyOUpRSHhROTkyTmhITGE0MFp2Y1JoMmlsM1Q2WmJ1R1JyS3p2bHhuaVpKWXVuVUZham43c3FOWVNVY2xON01XTkVNdzV1eHBCdTcwbExhMjU2anh1K0lNcFVOeU9tY2hjanRTVXZpYStMcnhMTmd3PT0tLWN4MzhobStsckhheGZRRmpCQTJTS1E9PQ%3D%3D--8274179183ee126234b96358f290b380794966c1; path=/; secure; HttpOnly
X-Request-Id: 0d95e9e6-4a2d-4e4a-bad6-d0424b30b30c
X-Runtime: 0.021043
Strict-Transport-Security: max-age=15552000; includeSubDomains
Strict-Transport-Security: max-age=15768000
Content-Encoding: gzip
```

