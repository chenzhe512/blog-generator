---
title: git简述
date: 2018-05-24 18:32:51
tags:
---
# <font color=black size=8>Git</font>
![](https://raw.githubusercontent.com/chenzhe512/blog-generator/master/image/git.png)
刚接触git一周左右的时间，看到这幅阮一峰老师的图片，感觉可以很清晰的解释git一些基本操作指令之间的关系，也说一下自己的了解：首先在本地先初始化或者新建一个仓库（用git init命令），git add是将自己在工作区的变动提交到暂存区，git commit是将暂存区的内容提交到本地仓库。至此，自己所进行的操作已经储存在了本地仓库。
# git init
```
$ git init
Initialized empty Git repository in C:/Users/Administrator/Desktop/music/.git/
```
初始化的空git仓库已经建立在C:/Users/Administrator/Desktop/music/.git/
# git add
```
Chenzhe@Chenzhe MINGW64 ~/desktop/music (master)
$ touch 666.txt
Chenzhe@Chenzhe MINGW64 ~/desktop/music (master)
$ git add 666.txt
```
创建一个666.txt的txt文件，并将其提交到暂存区
# git commit
```
$ git commit 666.txt -m "将666.txt从暂存区提交到本地仓库"
[master (root-commit) 24b7b50] 将666.txt从暂存区提交到本地仓库
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 666.txt
```
把暂存区的666.txt提交到本地仓库