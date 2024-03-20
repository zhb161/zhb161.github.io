---
layout:  post
title:   typora设置高亮快捷键
date:   2024-03-18 18:30:10
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-开发工具
-学习
-java

---


#### 自定义快捷键

1. 偏好设置-通用-高级设置-打开高级设置


![img](https://img-blog.csdnimg.cn/img_convert/455646e62f0ed7a670859db04e4cb147.png)

1. 打开conf.user.json


![img](https://img-blog.csdnimg.cn/img_convert/572d9922bc20ceba608820bd58ac9b58.png)

1. 找到keyBinding
2. 在keyBinding中添加"Highlight": "Ctrl + g"

```java
"keyBinding": {
    // for example: 
    // "Always on Top": "Ctrl+Shift+P"
    "Highlight": "Ctrl + g" 
  },
```


![img](https://img-blog.csdnimg.cn/img_convert/132475d90f07c6125c6086f399b0dc5e.png)

1. 重启typora，完成


![img](https://img-blog.csdnimg.cn/img_convert/0a596751df3beef112f15776f80e0a28.png)

