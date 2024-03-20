---
layout:  post
title:   idea debug调试时，显示未用变量存储的方法的返回值
date:   2023-05-31 15:39:36
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-开发工具
-idea
-单元测试
-java

---

在调试过程中，会遇到某些方法的返回值没有用变量存储，在debug时看不到返回值。比如返回值作为条件判断，或者返回值直接被return出去。这个时候就需要直接显示方法返回值。

## 1 打开方式

在debug工具框中，找到设置按钮：


![img](https://img-blog.csdnimg.cn/853c9ef6f8da4b6881d11da364d0cd53.png)

&nbsp;勾选show method return values


![img](https://img-blog.csdnimg.cn/7bb23f9bfc94453f9c9d33f756b5996a.png)

之后就可以在调试中看到方法的返回值了。

## 2 注意事项

注意，如果debug窗口小，设置不显示，点击&gt;&gt;就能看到设置，注意不要误点到其他几个按钮：


![img](https://img-blog.csdnimg.cn/a054a2042523498b94d08598240c71ea.png)

点击&gt;&gt;时很容易误点到其他按钮：


![img](https://img-blog.csdnimg.cn/da5320d178de4e578219d861f169c36f.png)&nbsp;这个是被误点后的样子，图中选中的按钮是禁用断点的意思，选中后是灰色框，这样就调试不了。


![img](https://img-blog.csdnimg.cn/9ecdb1756e584b44a5a5aad08305e503.png)

## 3 测试


![img](https://img-blog.csdnimg.cn/07be413a56c940b0a2cfa96f2911da40.png)

&nbsp;在两个断点出分别能看到下图结果，调试成功


![img](https://img-blog.csdnimg.cn/6b895dd495b94c0cbd6fd923611d2c57.png)


![img](https://img-blog.csdnimg.cn/7a21db9e68e1409c84fd18f73b99af86.png)



