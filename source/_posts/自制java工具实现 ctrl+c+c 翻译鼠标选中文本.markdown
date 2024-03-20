---
layout:  post
title:   自制java工具实现 ctrl+c+c 翻译鼠标选中文本
date:   2024-01-02 17:23:00
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-java日常
-java
-计算机外设
-学习

---


## 前言

>本功能的实现基于这篇笔记 <a href="http://t.csdnimg.cn/1I8ln" rel="nofollow">http://t.csdnimg.cn/1I8ln</a>，本文阅读过程中有疑惑都可以查看此笔记

>实现思路：检测到按压ctrl +c +c 后，获取当前剪切板文字，调用百度翻译api。

>实现结果：


![img](https://img-blog.csdnimg.cn/img_convert/ff245149703b143ded382a531038fd40.gif)

>完整代码在最后

## 实现过程

### 1 监控ctrl +c +c






在当前demo的功能中我们可以看到，当按压键盘时会调用nativeKeyPressed方法，并会打印当前按下的按钮字符串。![img](https://img-blog.csdnimg.cn/img_convert/2d88df6e2dfc1217d8e251da0b734d80.png)
 我们去掉一些打印的干扰：去除release和type的打印，以及press打印的前缀![img](https://img-blog.csdnimg.cn/img_convert/9705a1498f4aae7ec9c1c78e06b4d2a9.png)
 此时就只会打印我们的按键![img](https://img-blog.csdnimg.cn/img_convert/aae9d4cc19f29ecedb77ffafe69638b1.png)
 现在去实现：**当连续按压ctrl+c+c时，打印"你按下了ctrl+c+c哦"**
 思路：初始设置一个key字符串为"“,当检测到按压ctrl时，设置key为"Ctrl”，当不是Ctrl时，key拼接本次按压的按键，然后和"CtrlCC"做比较。如果相同，则说明用户连续按压了ctrl+c+c；**代码实现**（红框内为添加的代码）：![img](https://img-blog.csdnimg.cn/img_convert/bedef91c497647cf9b5f53de643e7f42.png)**效果：**![img](https://img-blog.csdnimg.cn/img_convert/282cfcd5fab9e67796ebf9db239ce244.png)

### 2 获取剪切板内容

在我们进行ctrl+c+c的操作过程中，第一个ctrl+c就会将鼠标选择的内容放到剪切板里，此时我们获取剪切板的内容，之后再用这个内容调用翻译api即可。**创建一个剪切板工具类**

```java
/**
 * 剪切板工具类
 */
public class ClipBoardUtil {
    public static String getClipboardText() {
        Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
        //从系统剪切板中获取数据
        Transferable content = clipboard.getContents(null);
        //判断是否为文本类型
        if (content.isDataFlavorSupported(DataFlavor.stringFlavor)) {
            //从数据中获取文本值
            String text = null;
            try {
                text = (String) content.getTransferData(DataFlavor.stringFlavor);
            }  catch (Exception e) {

            }
            if (text == null) {
                return "剪切板为空";
            }
            return text;
        }
        return "剪切板无文本值";
    }
}
```



**在代码中调用：**![img](https://img-blog.csdnimg.cn/img_convert/dab93c7cbfe1e1e221bd34461a849625.png)**效果：**![img](https://img-blog.csdnimg.cn/img_convert/e7922afe5131bb4c6473a67f631a1bbd.png)

### 3 调用百度翻译api

#### 注册账号，开通服务




搜索百度翻译开放平台，注册账号，实名认证后，可以申请高级版用户
 标准版：注册，未实名
 高级版：注册，实名
 尊享版：企业认证![img](https://img-blog.csdnimg.cn/img_convert/a7740099af16cd7b04ed41d02e7cb7db.png)
 高级版每个月有100万字符的免费调用量，对于个人使用的话绰绰有余了。
 注册后，在管理控制台中开通文本翻译服务![img](https://img-blog.csdnimg.cn/img_convert/219f1d5ae73f721423c8951356603742.jpeg)**详细见文档**：![img](https://img-blog.csdnimg.cn/img_convert/aa5c02e92d8d851a99ecc9421865d94b.png)

#### 根据文档，编写代码



![img](https://img-blog.csdnimg.cn/img_convert/1d27860a70ff11627a4ff7df2b0a9fd3.png)
 其中appid和密钥，在我们的管理控制台中![img](https://img-blog.csdnimg.cn/img_convert/8f8b995eec4b322945d0e67ea0d1b8d4.png)
 以下是调用方法的代码实现，我们创建一个TransApi类

```java
import cn.hutool.crypto.digest.DigestUtil;
import cn.hutool.http.HttpUtil;

import java.util.HashMap;
import java.util.Map;

public class TransApi {
    private static final String TRANS_API_HOST = "http://api.fanyi.baidu.com/api/trans/vip/translate";
    private String appid;
    private String securityKey;

    /**
     * 有参构造
     * @param appid appid
     * @param securityKey 密钥
     */
    public TransApi(String appid, String securityKey) {
        this.appid = appid;
        this.securityKey = securityKey;
    }
    
    /**
     * 调用方法
     * @param query 翻译内容
     * @param from 来源语言
     * @param to 翻译语言
     * @return 返回参数
     */	
    public String getTransResult(String query, String from, String to) {
        Map<String, Object> params = this.buildParams(query, from, to);
        return HttpUtil.get("http://api.fanyi.baidu.com/api/trans/vip/translate", params);
    }

    /**
     * 初始化参数
     * @param query 翻译内容
     * @param from 来源语言
     * @param to 翻译语言
     * @return
     */
    private Map<String, Object> buildParams(String query, String from, String to) {
        Map<String, Object> params = new HashMap();
        params.put("q", query);
        params.put("from", from);
        params.put("to", to);
        params.put("appid", this.appid);
        String salt = String.valueOf(System.currentTimeMillis());
        params.put("salt", salt);
        String src = this.appid + query + salt + this.securityKey;
        //MD5加密
        params.put("sign", DigestUtil.md5Hex(src));
        return params;
    }
}
```

其中调用接口的HttpUtil和加密的DigestUtil使用的是hutool中的类
 hutool包的地址：

```java
<dependency>
  <groupId>cn.hutool</groupId>
  <artifactId>hutool-all</artifactId>
  <version>5.8.24</version>
</dependency>
```

#### ctrl+c+c获取剪切板内容并调用翻译接口



在GlobalKeyListenerExample类中添加TransApi类的初始化：![img](https://img-blog.csdnimg.cn/img_convert/ab42880b2223f2a1717257a024e8f792.png)
 在获取剪切板内容后，将剪切板的内容调用翻译接口，并**处理返回数据**![img](https://img-blog.csdnimg.cn/img_convert/ee7dbbd6929a42dbe278da245d894cea.png)

#### 运行效果


![img](https://img-blog.csdnimg.cn/img_convert/daa04cb114e95551f535b18f8735a7f7.png)
 我们看到这里，已经初步完成了**ctrl+c+c进行翻译**的功能，剩下的就是进行一些小优化，如生成窗口展示数据

### 4 小窗口展示剪切板内容和翻译内容

因为笔者对java的gui窗口不是很了解，这里使用chatgpt工具生成了小窗口，可能有些简陋，读者可以自己美化一下
 新建一个MyWindows类

```java
import javax.swing.*;
import java.awt.*;

public class MyWindow extends JFrame {

    private JTextArea textArea;

    public MyWindow() {
        setTitle("Text Window");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        textArea = new JTextArea();
        //设置字体大小
        textArea.setFont(new Font("SimSun", Font.PLAIN, 16));
        // 自动换行
        textArea.setLineWrap(true);
        // 断行不断字
        textArea.setWrapStyleWord(true);
        JPanel panel = new JPanel();

        setVisible(true);
        add(textArea, "Center");
        add(panel, "South");
    }

    //写入文本
    public void writeText(String text) {
        textArea.append(text + "\n");
    }
    //清楚文本
    public void clearText() {
        textArea.setText("");
    }

    public static void main(String[] args) {
        MyWindow window = new MyWindow();
        window.setVisible(true);
    }
}
```




在GlobalKeyListenerExample类中初始化MyWindow：![img](https://img-blog.csdnimg.cn/img_convert/2dfe3308c6c16d9d99949cf0fde61c29.png)
 在获取翻译后，清除原来的文字，写入新的文字：![img](https://img-blog.csdnimg.cn/img_convert/56d29b77a5fdc44fcdb76ae08b6d1cd4.png)
 运行：![img](https://img-blog.csdnimg.cn/img_convert/ff245149703b143ded382a531038fd40.gif)

## 完整代码

ClipBoardUtil类，TransApi类，MyWindow类上文已給出完整代码。GlobalKeyListenerExample类：

```java
import cn.hutool.core.text.UnicodeUtil;
import cn.hutool.json.JSONObject;
import cn.hutool.json.JSONUtil;
import com.github.kwhat.jnativehook.GlobalScreen;
import com.github.kwhat.jnativehook.NativeHookException;
import com.github.kwhat.jnativehook.keyboard.NativeKeyEvent;
import com.github.kwhat.jnativehook.keyboard.NativeKeyListener;
import com.icepeach.Utils.ClipBoardUtil;
import com.icepeach.Utils.GUI.MyWindow;


public class GlobalKeyListenerExample implements NativeKeyListener {
    String key = "";
    private static final String APP_ID = "你的appid";
    private static final String SECURITY_KEY = "你的密钥";
    TransApi api = new TransApi(APP_ID, SECURITY_KEY);
    MyWindow window = new MyWindow();

    public void nativeKeyPressed(NativeKeyEvent e) {


        if ("Ctrl".equals(NativeKeyEvent.getKeyText(e.getKeyCode()))) {
            key = new String("Ctrl");
        } else {
            key += NativeKeyEvent.getKeyText(e.getKeyCode());
        }

        if ("CtrlCC".equals(key)) {
            window.setVisible(true);
            //打印剪切板内容
            System.out.println("剪切板内容为：" + ClipBoardUtil.getClipboardText());
            //调用翻译接口
            String jsonStr = api.getTransResult(ClipBoardUtil.getClipboardText(), "auto", "zh");
            // 解析JSON字符串
            JSONObject jsonObject = JSONUtil.parseObj(jsonStr);
            // 获取trans_result数组中的第一个元素
            JSONObject transResult = jsonObject.getJSONArray("trans_result").getJSONObject(0);
            // 获取dst中的内容并转换成中文
            String dst = transResult.getStr("dst");
            String chineseDst = UnicodeUtil.toString(dst);

            System.out.println("翻译:"+chineseDst);


            window.clearText();
            window.writeText("剪切板内容为：" + ClipBoardUtil.getClipboardText());
            window.writeText("翻译:"+chineseDst);

        }
        if (e.getKeyCode() == NativeKeyEvent.VC_ESCAPE) {
            try {
                GlobalScreen.unregisterNativeHook();
            } catch (NativeHookException nativeHookException) {
                nativeHookException.printStackTrace();
            }
        }
    }

    public void nativeKeyReleased(NativeKeyEvent e) {
//        System.out.println("Key Released: " + NativeKeyEvent.getKeyText(e.getKeyCode()));
    }

    public void nativeKeyTyped(NativeKeyEvent e) {
//        System.out.println("Key Typed: " + e.getKeyText(e.getKeyCode()));
    }

    public static void main(String[] args) {
        try {
            GlobalScreen.registerNativeHook();
        } catch (NativeHookException ex) {
            System.err.println("There was a problem registering the native hook.");
            System.err.println(ex.getMessage());

            System.exit(1);
        }

        GlobalScreen.addNativeKeyListener(new GlobalKeyListenerExample());
    }
}
```

