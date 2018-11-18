---
title: Cookie、Session等
date: 2018-09-21 01:52:59
tags:
---
# 题
Cookie 和 Session 的区别：
Cookie 保存在客户端，每次都随请求发送给 Server

Session 保存在 Server 的内存里，其 Session ID 是通过 Cookie 发送给客户端的

Cookie 和 LocalStorage 的区别：
LocalStorage 不会随 HTTP 发给 Server
LocalStorage 的大小限制比 Cookie 大多了

LocalStorage 和 SessionStorage 的区别：
一个不会自动过期，一个会自动过期。

Cookie 如何设置过期时间？
如何删除 Cookie？

学生的回答
Set-Cookie: name=Nicholas; expires=Sat, 02 May 2009 23:38:25 GMT //没有expires的话，关闭页面后立即清理cookie，有的话，后面设置一个到期的事件

删除cookie就把上面设置cookie里的时间设置为一个已经过去的时间就会删除

Cache-Control: max-age=1000 缓存 与 ETag 的「缓存」有什么区别？

参考答案
Cache-Control 直接不发请求。
而 ETag 要发请求才行。
