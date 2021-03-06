---
title: Vim和MD
date: 2018-05-30 11:07:17
tags:
---
>一直想写一下MD的语法来让自己加深一下了解，系统整理一下加深记忆。Vim中也有很多问题不明白操作原理、快捷键作用。但两个知识日常中用到的很多，所以总结一下。
# Markdown
## 定义
Markdown是一种轻量级标记语言（语法格式简单一些），它允许人们使用易读易写的纯文本格式来编写文档，然后转换成有效的XHTML(HTML)文档。[维基百科]
## 语法
### 图片
`![图片名称](图片链接)`
### 链接
`[链接文字](链接地址)`
### 换行
在文本中输入的换行最终会被删除，浏览器会根据自身需要来进行换行。如果想进行强制换行，可以在结尾**插入至少两个空格再换行**。
### 粗斜
```
*加斜*  _加斜_
**加粗**  __加斜__
***加粗并加斜***
```
### 标题
```
# 一级标题
## 二级标题
……
```
（#和标题间有一个空字符）
### 引用
在引用的段落前加上右尖括号即可<kbd>><kbd>
### 水平分区线
水平分区线可以由三个或三个以上<kbd>*<kbd>、<kbd>-<kbd>和<kbd>_<kbd>来实现，即星号、短横线和下划线。
### 列表
无序列表可以由<kbd>*<kbd>、<kbd>-<kbd>、<kbd>+<kbd>中的任意一个符号加空格进行创建。   
有序列表可以由**数字+点+空格**来创建。
### 代码段
使用<kbd>`<kbd>来实现，开头结尾都要用3个或以上来实现多行代码，要换行。
### 表格
使用<kbd>-<kbd>和<kbd>|<kbd>来实现。例如：
```
表头1|表头2|表头3
:----|:-----:|-----:
左对齐|居中对齐|右对齐
```
表头1|表头2|表头3
:----|:-----:|-----:
左对齐|居中对齐|右对齐
********************
# Vim
## 基本了解
Vim(简称vi)分为三种状态，分别是命令模式、插入模式、底行模式。
### 命令行模式(command mode)
控制屏幕光标的移动，字符、字或行的删除，移动复制某区段及进入插入模式(Insert mode)下，或者到底行模式(last line mode)。
### 插入模式（Insert mode）
只有在Insert mode下，才可以做文字输入，按「ESC」键可回到命令行模式。
### 底行模式(last line mode)
将文件保存或退出vi，也可以设置编辑环境，如寻找字符串、列出行号……等.
## 基本操作
### 如何进入vi
在系统提示符号输入vi及文件名称后，就进入vi全屏幕编辑画面
`$ vi myfile`
### 切换至插入模式
进入vi后是处于命令行模式下，需要切换至插入模式才能编辑文本，在命令行模式下按一下字母「i」就可以进入插入模式。
### 删除文字
处于插入模式下只能一直输入文本，删除文字时需要切换至命令行模式才能进行删除，按一下「ESC」键转到命令行模式再删除文字。
### 退出及保存
在命令行模式下，按一下「：」冒号键进入底行模式，例如：
: w filename （输入 「w filename」将文章以指定的文件名filename保存）
: wq (输入「wq」，存盘并退出vi)
: q! (输入q!， 不存盘强制退出vi)
## vi按键图示
![VI](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/vim.jpg)
