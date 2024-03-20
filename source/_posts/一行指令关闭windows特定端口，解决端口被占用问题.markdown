---
layout:  post
title:   一行指令关闭windows特定端口，解决端口被占用问题
date:   2024-03-18 18:30:00
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-一键系列
-windows
-网络

---


#### 1：一条代码

```java
Get-Process -Id (Get-NetTCPConnection -LocalPort 10001).OwningProcess | Stop-Process -Force
```

注意：get-process命令需要打开Powershell终端才能运行


![img](https://img-blog.csdnimg.cn/img_convert/afdf2fc85c7e6274e56129ae0b43c5d8.png)

**解释：**

- 
 这是一条 PowerShell 命令，用于根据本地端口号查找对应的进程并强制结束它。下面是该命令的详细解释：
 <ul>
  - 
   Get-NetTCPConnection -LocalPort 10001：使用 Get-NetTCPConnection 命令查找本地使用 10001 端口的 TCP 连接。该命令返回了与该端口相关联的网络连接（如果有）。-LocalPort 参数指定要查找的本地端口号。
  - 
   (Get-NetTCPConnection -LocalPort 10001).OwningProcess：从上一条命令的输出中取出 OwningProcess 属性的值，即与本地端口相关联的进程 ID。
  - 
   Get-Process -Id：使用 Get-Process 命令查找与指定的进程 ID 相关联的进程对象。
  - 
   | Stop-Process -Force：使用管道将输出传递给 Stop-Process 命令，强制结束指定的进程。-Force 参数表示强制结束进程，即使进程不响应也要结束。
 </ul>
 因此，该命令的作用是：查找本地端口号为 10001 的 TCP 连接，并通过该连接的 OwningProcess 属性获取进程 ID，然后使用 Get-Process 命令获取该进程对象，并将其传递给 Stop-Process 命令来强制结束该进程。这可以在需要停止指定端口上的进程时很有用。

因此，这个命令的意思是：使用 netstat 工具查找所有使用 10001 端口的连接，并将每个连接的进程 ID 作为参数传递给 taskkill 命令，以便强制结束该进程。可以用类似其他端口的情况使用，只需要替换 “10001” 为想要查找和终止进程的端口号即可。

#### 2：普通方法

我要关闭10001端口的进程：

```java
netstat -ano|findstr "10001"
```

结果：


![img](https://img-blog.csdnimg.cn/img_convert/fa0ce3e30a84e4aa8a38340b76fce07b.png)

5928就是使用这个端口的进程编码，我们关闭这个端口：

```java
taskkill /f /pid 5928
```

搞定

