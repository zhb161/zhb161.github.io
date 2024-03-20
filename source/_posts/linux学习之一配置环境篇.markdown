---
layout:  post
title:   linux学习之一配置环境篇
date:   2023-05-31 15:35:17
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-linux
-linux
-学习
-运维

---


### 前言

一般来说，配置linux有两种方法，第一种是在各大云服务厂商**购买云服务器**，在本地通过xshell等远程连接软件调用。很多厂商对学生是有补贴的，比如阿里云有学生试用三个月的活动，这一方法的**优点**是它最接近工作之后对linux服务器的使用。**缺点**是有可能需要一些小钱钱。

第二种就是在**本地**通过**虚拟机安装linux**系统，然后ping通物理机和虚拟机，之后通过xshell连接虚拟机中的linux进行学习（当然也可以直接在虚拟机的linux通过命令行学习）。这一方法的优点是免费，缺点是可能需要折腾，会出现各种各样的问题

### 我的配置

我是使用的第二种方法，在本地安装虚拟机。

我为大家准备了尚硅谷的安装文档，我就是完全这个安装文档来进行配置的。

阿里云盘：https://www.aliyundrive.com/s/qeWFkJeKf6r


![img](https://img-blog.csdnimg.cn/img_convert/42dad5568bf83a6d184d21574a85b1ce.png)

>为什么使用阿里云盘：因为阿里云盘不限制下载速度。

虚拟机使用的是 **VMware Workstation**，这也是最常用的一个虚拟机，安装包也在上述云盘中，大家只需要根据安装教程安装，且最后在网上寻找一下密钥即可。

寻找密钥方式如下（百度搜索）：


![img](https://img-blog.csdnimg.cn/img_convert/a7e23604086f1f8f22530e2220ee18e5.png)

同时linux的镜像文件也放在了云盘的文件中，各位只要根据文档安装配置，大概率是可以一次成功的。（笔者就是一次成功，没有什么波折）。

根据文档安装完成图：


![img](https://img-blog.csdnimg.cn/img_convert/952b3fea3c342d89848dc5552c3737ed.png)

之后的学习就看下一篇：

linux学习之二基础命令篇

