---
layout:  post
title:   linux学习之二基础命令篇
date:   2024-03-18 16:32:21
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-linux
-学习
-服务器

---


## 一 linux的目录结构

### 学习目标

>1 掌握linux系统的目录结构

### linux的目录结构


Linux的目录结构是一个树型结构
 Windows 系统可以拥有多个盘符, 如 C盘、D盘、E盘
 Linux没有盘符这个概念, 只有一个根目录 /, 所有文件都在它下面![img](https://img-blog.csdnimg.cn/7ae9f2547cd84ccbb28ad850e8f8d5d0.png)

### Linux路径的描述方式

- 在Linux系统中，路径之间的层级关系，使用：/ 来表示
- 在Windows系统中，路径之间的层级关系，使用： \ 来表示**windows:**


![img](https://img-blog.csdnimg.cn/72602aa5526f481a8004e72d8a4c5d0d.png)**D:\data\work\hello.txt**

- 注意：
- D:表示D盘
- \表示层级关系


**linux:**![img](https://img-blog.csdnimg.cn/da1ffc24bcf64bd3a7b5901de6c41c0c.png)**/usr/local/hello.txt**

- 注意：
- 开头的/表示根目录
- 后面的/表示层级关系

### 总结

1. Linux操作系统的目录结构
    Linux只有一个顶级目录，称之为：根目录
    Windows系统有多个顶级目录，即各个盘符
<li>在Linux系统中表示
    出现在开头的/表示：根目录
    出现在后面的/表示：层次关系</li>

### 课后练习

请根据语言描述，写出对应的Linux路径

- 在根目录下有一个文件夹test，文件夹内有一个文件hello.txt，请描述文件的路径
  /test/hello.txt
- 在根目录下有一个文件itheima.txt，请描述文件的路径
  /itheima.txt
- 在根目录下有一个文件夹itcast，在itcast文件夹内有文件夹itheima，在itheima文件夹内有文件hello.txt，请描述文件的路径
  /itcast/itheima/hello.txt

## 二 linux命令入门

### linux命令基础格式

无论是什么命令，用于什么用途，在Linux中，命令有其通用的格式：command [-options] [parameter]

- command： 命令本身
- -options：[可选，非必填]命令的一些选项，可以通过选项控制命令的行为细节
- parameter：[可选，非必填]命令的参数，多数用于命令的指向目标等

 *语法中的[]，表示可选的意思* 

### ls命令

ls命令的作用是列出目录下的内容，语法细节如下：ls [-a -l -h] [linux路径]


- -a -l -h 是可选的选项
- Linux路径是此命令可选的参数
  当不使用选项和参数，直接使用ls命令本体，表示：以平铺形式，列出当前工作目录下的内容![img](https://img-blog.csdnimg.cn/c09af8949939427a9fe7f38eb8017bda.png)

### home目录和工作目录


直接输入ls命令，表示列出当前工作目录下的内容，当前工作目录是？![img](https://img-blog.csdnimg.cn/c09af8949939427a9fe7f38eb8017bda.png)
 Linux系统的命令行终端，在启动的时候，默认会加载:

- 当前登录用户的HOME目录作为当前工作目录，所以ls命令列出的是HOME目录的内容
- HOME目录：每个Linux操作用户在Linux系统的个人账户目录，路径在：/home/用户名 
 <ul>
  - 如，图中的Linux用户是root，其HOME目录是：/home/root
  - Windows系统和Linux系统，均设有用户的HOME目录，如图：
 </ul>



![img](https://img-blog.csdnimg.cn/3e4d8500ce054f2bb173d6e9f1af8dd5.png)![img](https://img-blog.csdnimg.cn/dd7ae71dafb34eeb82eea490840c1ae6.png)

### ls命令的参数


刚刚展示了，直接使用ls命令，并未使用选项和参数。
 那么ls的选项和参数具体有什么作用呢？首先我们先来看参数。
 当ls不使用参数，表示列出：当前工作目录的内容，即用户的HOME目录
 当使用参数，ls命令的参数表示：指定一个Linux路径，列出指定路径的内容
 如![img](https://img-blog.csdnimg.cn/8872dbcbaedb41318ab5e07e74261ca8.png)
 通过ls / 列出了根目录的内容

### ls命令的选项



- -a选项，表示：all的意思，即列出全部文件（包含隐藏的文件/文件夹）
- -l选项，表示：以列表（竖向排列）的形式展示内容，并展示更多信息
- -h 表示以易于阅读的形式，列出文件大小，如K、M、G
- -h选项必须要搭配 -l 一起使用![img](https://img-blog.csdnimg.cn/5c97357073f04df18fa62e8183866fa3.png)
  -l -h 搭配使用![img](https://img-blog.csdnimg.cn/e5d2238ecf0748da8e750c9fadc0d6dc.png)

>注：<br>
 语法中的选项是可以组合使用的，比如学习的-a和-l可以组合应用。

### 总结

1. Linux命令的基础格式command [options] [parameter]
2. ls命令的语法和作用

- command [-a -l -h] [linux路径]
- -a列出全部内容、-l以列表展示、-h更易读的大小显示
- 参数表示要列出内容的路径，不提供即列出当前工作目录内容

1. 当前工作目录和HOME目录

- Linux终端（命令行）启动后默认价值HOME目录作为当前工作的目录
- HOME目录指：用户在系统内的专属目录

1. 隐藏文件\文件夹

- 在Linux系统中，以”.”开头的文件\文件夹会自动隐藏
  只有通过-a选项才可以展示出来

## 三 目录切换相关命令

### cd切换工作目录当Linux终端（命令行）打开的时候，会默认以用户的HOME目录作为当前的工作目录

我们可以通过cd命令，更改当前所在的工作目录。
 cd命令来自英文：Change Directory
 语法： cd [linux路径]


- cd命令无需选项，只有参数，表示要切换到哪个目录下
- cd命令直接执行，不写参数，表示回到用户的HOME目录![img](https://img-blog.csdnimg.cn/de9907a5214745958cd664b19168f48a.png)

