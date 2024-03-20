---
layout:  post
title:   html中元素的隐藏，以及用jquery来显示和隐藏元素
date:   2024-03-18 19:21:30
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-前端
-jquery
-html
-前端

---


添加一个属性：style="display:none;"

```java
<td id="tdTest" style="display:none;">//默认隐藏
<input type="text" id="inputtest">//默认显示
<script>
    //显示td
    $("#tdTest").show();
    //隐藏td和input
    $("#tdTest").hide();
    $("#inputtest").hide();
    //显示input
    $("#inputtest").show();
    
    //注：除此之外，表单元素还可以通过type属性来隐藏
	//隐藏input
     $("#inputtest").attr("type","hidden");
</script>
```

