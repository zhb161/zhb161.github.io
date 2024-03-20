---
layout:  post
title:   安装完vue-cli后 在控制台输入vue 显示‘vue‘ 不是内部或外部命令，也不是可运行的程序 或批处理文件。
date:   2023-05-31 15:35:34
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-前端
-vue.js
-javascript
-前端

---


在使用 npm install -g @vue/cli 命令全局安装vue脚手架之后，关掉控制台重新打开后输入vue，显示
 显示’vue’ 不是内部或外部命令，也不是可运行的程序或批处理文件






**可能的解决办法：**
 在控制台运行npm config list 查看npm配置信息
 我的是这样：![img](https://img-blog.csdnimg.cn/e16d3c2df789452cbeb49e95e1ece622.png)
 找到prefix属性后的地址，到文件夹对应地址看一下里面有没有vue
 有的话，打开修改系统变量的地方：![img](https://img-blog.csdnimg.cn/16496742c2294be88c9efc82c3e3b055.png)![img](https://img-blog.csdnimg.cn/ad086eb541a64687ab5853a78e8d028e.png)
 找到系统变量中的path![img](https://img-blog.csdnimg.cn/8f5e979deb1047a79966695d4cd1a3c4.png)
 点击编辑，添加刚刚的地址![img](https://img-blog.csdnimg.cn/ef5894cd7e83435baf21a414a88236fe.png)

