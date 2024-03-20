---
layout:  post
title:   尚硅谷周阳spring cloud alibaba笔记
date:   2022-09-22 09:50:56
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-微服务
-spring cloud
-java
-后端

---


【尚硅谷SpringCloud框架开发教程(SpringCloudAlibaba微服务分布式架构丨Spring Cloud)】https://www.bilibili.com/video/BV18E411x7eT?p=97&amp;vd_source=10e3dfac95ac3a6883b1f8a6c3bc65d5

注：从spring cloud alibaba开始学习的，所以笔记只包含第十三章之后的部分
 持续更新中…




## nacos

### 一、nacos的安装和运行

访问官网https://nacos.io/zh-cn/

在前往GitHub下方的xxx版本说明处点击进入下载页面


点击releases![img](https://img-blog.csdnimg.cn/c8e3acbc41df4009b22e35f2b8e09ddd.png#pic_center)

点击Tags可以选择不同的版本（注：不同的版本和spring boot会相互对应）


![img](https://img-blog.csdnimg.cn/ed0e5e74da584a53ba00143fc0a7b3f0.png#pic_center)

本课程使用的 是1.1.4版本

下载完后解压安装包，在nacos文件夹中的bin文件夹中找到startup文件，双击运行。


![img](https://img-blog.csdnimg.cn/bb5e34d8183c4852903eb97466b68c69.png#pic_center)

访问localhost:8849/nacos，如果出现如下页面，则启动成功。


![img](https://img-blog.csdnimg.cn/f8f0cadd6bf94cca837f5966773c8df7.png#pic_center)

注：如果访问不成功，大概率是没有把默认的集结模式改成单例模式

修改方法：

 [青戈程序员_nacos——服务注册_abjtxf的博客-CSDN博客](https://blog.csdn.net/abjtxf/article/details/126965089#comments_23365646)中3 nacos的启动

登录账号密码都是nacos

### 二、nacos服务注册

使用之前写过的青戈程序员的方法，过程是一样的

 [青戈程序员_nacos——服务注册_abjtxf的博客-CSDN博客](https://blog.csdn.net/abjtxf/article/details/126965089#comments_23365646)

