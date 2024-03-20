---
layout:  post
title:   java全局监听键盘
date:   2024-01-02 17:22:14
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-java日常
-java
-计算机外设
-开发语言

---


## 前言

>在github上看一些开源的项目时，常常有一些英文单词和句子需要翻译，当前的翻译软件以及划词插件，多少都有一些弊端。比如翻译软件过于臃肿，划词插件只能在浏览器中使用，且不需要使用翻译功能时也会出现。

>deepl有一个ctrl+c+c自动悬浮翻译的功能，比较能满足我的需求，但很多时候因为deepl的悬浮翻译框都是在旋转的状态，网络上检索时，说是因为服务器问题。好吧。

>于是想自己写一个小工具，实现deepl ctrl+c+c翻译的功能。

java中的监听键盘的api，必须先创建一个窗口，且鼠标聚焦在该窗口中才能使用，无法实现我全局监听键盘的需求，于是在一番检索之后，找到了以下两个开源项目。system-hook： [https://github.com/kristian/system-hook](https://github.com/kristian/system-hook)jnativehook： [https://github.com/kwhat/jnativehook](https://github.com/kwhat/jnativehook)
 比较后，我选择了jnativehook,因为这个项目维护的较好，同时还有全局鼠标，全局鼠标滚轮等功能。

>ctrl+c+c翻译实现见这篇笔记：<a href="http://t.csdnimg.cn/See4F" rel="nofollow">http://t.csdnimg.cn/See4F</a><br>
 本文只介绍全局监听键盘实现方法

## 使用方法

在maven中添加地址：

```java
<dependency>
  <groupId>com.github.kwhat</groupId>
  <artifactId>jnativehook</artifactId>
  <version>2.2.2</version>
</dependency>
```



在项目主页找到demo代码：![img](https://img-blog.csdnimg.cn/img_convert/107972ecbcd5cab16c2e290374d83fc4.png)![img](https://img-blog.csdnimg.cn/img_convert/2237299f22ea0e1a5a972718ac253250.png)

```java
import com.github.kwhat.jnativehook.GlobalScreen;
import com.github.kwhat.jnativehook.NativeHookException;
import com.github.kwhat.jnativehook.keyboard.NativeKeyEvent;
import com.github.kwhat.jnativehook.keyboard.NativeKeyListener;

public class GlobalKeyListenerExample implements NativeKeyListener {
	public void nativeKeyPressed(NativeKeyEvent e) {
		System.out.println("Key Pressed: " + NativeKeyEvent.getKeyText(e.getKeyCode()));

		if (e.getKeyCode() == NativeKeyEvent.VC_ESCAPE) {
            		try {
                		GlobalScreen.unregisterNativeHook();
            		} catch (NativeHookException nativeHookException) {
                		nativeHookException.printStackTrace();
            		}
        	}
	}

	public void nativeKeyReleased(NativeKeyEvent e) {
		System.out.println("Key Released: " + NativeKeyEvent.getKeyText(e.getKeyCode()));
	}

	public void nativeKeyTyped(NativeKeyEvent e) {
		System.out.println("Key Typed: " + e.getKeyText(e.getKeyCode()));
	}

	public static void main(String[] args) {
		try {
			GlobalScreen.registerNativeHook();
		}
		catch (NativeHookException ex) {
			System.err.println("There was a problem registering the native hook.");
			System.err.println(ex.getMessage());

			System.exit(1);
		}

		GlobalScreen.addNativeKeyListener(new GlobalKeyListenerExample());
	}
}
```


运行后按键：![img](https://img-blog.csdnimg.cn/img_convert/c00aecbfe6a882f293abf1a8055fc544.png)

## 方法解析

1. nativeKeyPressed:当键盘上的某个键被按下时，这个函数会被调用。它首先打印出被按下的键的文本信息，然后检查是否是"Escape"键(即VC_ESCAPE常量的值),如果是，就尝试注销全局键盘钩子。如果在注销过程中发生异常，就会捕获并打印这个异常。
2. nativeKeyReleased:当键盘上的某个键被释放时，这个函数会被调用。它打印出被释放的键的文本信息。
3. nativeKeyTyped:当键盘上的某个键被输入时，这个函数会被调用。它打印出被输入的键的文本信息。

## 总结

当可以监听到键盘按键后，就可以实现一些对应的功能，比如开头说的**ctrl+c+c **翻译鼠标选中内容，或者按键模拟乐器等。

