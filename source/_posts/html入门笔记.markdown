---
layout:  post
title:   html入门笔记
date:   2024-03-18 19:21:30
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-前端
-html
-前端
-css

---


这是是在wuyxinu大佬的笔记里摘抄的，去掉了一些对我自己而言不怎么用得着的部分
 原笔记网址：http://t.csdn.cn/rEZHo

## 一、简介

### 1、前端开发最核心技术

(1)HTML

HTML，全称“Hyper Text Markup Language（超文本标记语言）”

(2)CSS

CSS，全称“（层叠样式表）”

(3)JavaScript

### 2、前端开发其他技术

(1)Ajax

Ajax，即“Asynchronous Javascript And XML（异步JavaScript和XML）”，是指一种创建交互式网页应用的网页开发技术。

可以在不重新加载整个网页的情况下，对网页的某部分进行更新。传统的网页（不使用Ajax）如果需要更新内容，必须重载整个页面。

(2)SEO

SEO，即“Search Engine Optimization（搜索引擎优化）”。利用搜索引擎的搜索规则来提高目前网站在有关搜索引擎内的自然排名的方式

## 二、基础内容

### 1.基础总结

HTML基本结构：


![img](https://imgconvert.csdnimg.cn/aHR0cDovL3d3dy5sdnllc3R1ZHkuY29tL0FwcF9pbWFnZXMvbGVzc29uL2hqLzMtMS0xLnBuZw?x-oss-process=image/format,png)

### 2.HTML的基本标签

#### (1)HTML标签

整个网页是从这里开始的，然后到结束。

#### (2)head标签

head标签代表页面的“头”，定义一些特殊内容，这些内容往往都是“不可见内容”（在浏览器不可见）。


#### (3)body标签

代表页面的“身”，定义网页展示内容，这些内容往往都是“可见内容”（在浏览器可见）。

后续课程讲解的标签都是在标签内部的各种标签。

### 3、段落与文字

#### (一)、段落标签

**(1)、段落与文字标签**


**(2)、文本格式化标签**


#### (二)、网页特殊符号

#### (三)、自闭合标签

HTML标签分为2种，一种是“一般标签”，另外一种是“自闭合标签”。一般标签有开始符号和结束符号，自闭合标签只有开始符号没有结束符号。

一般标签可以在开始符号和结束符号之间插入其他标签或文字。

自闭合标签由于没有结束符号，不能插入其他标签或文字，只能定义自身的属性。

**(1)、一般标签**

举例：

**(2)、自闭合标签**

举例：<br/>、<hr/>

#### (四)、块元素和行内元素

(1)、HTML元素根据浏览器表现形式分为两类：①块元素；②行内元素；

(2)、块元素特点：

（1）独占一行，排斥其他元素跟其位于同一行，包括块元素和行内元素；
 （2）块元素内部可以容纳其他块元素或行元素；
 常见块元素有：h1~h6、p、hr、div等。

(3)、行内元素特点：

（1）可以与其他行内元素位于同一行；
 （2）行内内部可以容纳其他行内元素，但不可以容纳块元素，不然会出现无法预知的效果；
 常见行内元素有：strong、em、span等。

### 4、列表

**(1)、有序列表**

```java
<ol>
    <li>有序列表项</li>
    <li>有序列表项</li>
    <li>有序列表项</li>
</ol>
```

**(2)、无序列表**

```java
<ul  type="列表项符号">
    <li>无序列表项</li>
    <li>无序列表项</li>
    <li>无序列表项</li>
</ul>
```

### 5、表格

#### (一)、表格语义记忆

1 表格基本标签：


2 表格结构标签：


#### (二)、表格基本结构

```java
<table>
    <tr>
        <td>单元格1</td>
        <td>单元格2</td>
    </tr>
    <tr>
        <td>单元格1</td>
        <td>单元格2</td>
    </tr>
</table>
```

#### (三)、表格完整结构

```java
<table>
    <caption>表格标题</caption>
    <!--表头-->
    <thead>
        <tr>
            <th>表头单元格1</th>
    <th>表头单元格2</th>
        </tr>
    </thead>
    <!--表身-->
    <tbody>
        <tr>
            <td>标准单元格1</td>
            <td>标准单元格2</td>
        </tr>
        <tr>
            <td>标准单元格1</td>
            <td>标准单元格2</td>
        </tr>
    </tbody>
    <!--表脚-->
    <tfoot>
        <tr>
            <td>标准单元格1</td>
            <td>标准单元格2</td>
        </tr>
    </tfoot>
</table>
```

### 6、图像

#### (一)、图像标签

在HTML中，图像标签为。是一个自闭合标签。 [img标签](http://www.lvyestudy.com/les_hj/hj_7.1.aspx)只需要掌握3个属性就可以了：src、alt、title。

语法：

<img src="图片地址" alt="图片描述（给搜索引擎看）" title="图片描述（给用户看）">

alt:图片显示不出来时的提示文字

title:鼠标移到图片上的提示文字

#### (二)、相对路径和绝对路径

相对路径，指的是同一个网站下，不同文件之间的的位置定位。引用的文件位置是相对当前文件的位置而言，从而得到相对路径。

绝对路径，指的是文件的完整路径。

详细复习内容，请查看 [相对路径和绝对路径](http://www.lvyestudy.com/les_hj/hj_7.2.aspx)。

### 7、链接

超链接使用 [a标签](http://www.lvyestudy.com/les_hj/hj_8.2.aspx)，语法如下：


#### target属性值：

1 _self：默认方式，即在当前窗口打开链接

2 _blank：在一个全新的空白窗口中打开链接

#### href

超链接根据链接对象的不同分为：

**（1）外部链接**

从自己的网站跳转到别人的网站

**（2）内部链接：**

①内部页面链接；

在自己的网站中，网页之间相互跳转。<a href="a.html" target="_blank">跳转到a.html</a>

②锚点链接；

跳转到当前网页指定的位置

先给要跳转的位置标签设置id属性

在a标签的href属性中写#id

```java
<h2 id=“one”>第一层</h2>
<a href="#one">去第一层</a>
```

**（3）空链接**

当还没有想好跳转到哪里时,在href中写#号。写一个#号会回到本网页的顶部，写两个#号单击了链接也不发生变化。

```java
<a href="#">回到本网页的顶部</a>
<a href="##">单击了链接也不发生变化</a>
```

### 8、表单

表单标签共有4个：、、和。其中和是配合使用的。

#### (一)、input标签表单


![img](https://img-blog.csdnimg.cn/img_convert/8595c9fd77ab2ca0bf3276a54682736a.png)

#### (二)、textarea标签表单

```java
<textarea rows="行数" cols="列数">多行文本框内容</textarea>
```

#### (三)、select和option

```java
<select multiple="mutiple" size="可见列表项的数目">
    <option value="选项值" selected="selected">选项显示的内容</option>
    ……
    <option value="选项值">选项显示的内容</option>
</select>
```

https://blog.csdn.net/wuyxinu/article/details/103583618#t13

