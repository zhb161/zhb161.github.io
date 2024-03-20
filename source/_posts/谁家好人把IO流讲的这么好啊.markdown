---
layout:  post
title:   谁家好人把IO流讲的这么好啊
date:   2023-12-04 21:58:47
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-java基础知识
-java
-开发语言
-学习

---


>本笔记知识点来源

## 引子

IO流说白了就是对文件的一系列操作，这里我用一个简单的例子展示IO流的使用

**需求：**

把e盘的我是源文件.txt文件复制一份，在e盘创建一个目录：我是一个目录,把源文件粘贴在这个目录中，给新文件起名为我是新文件.txt


![img](https://img-blog.csdnimg.cn/img_convert/c8d6ec7d97236718064c725320b249c1.png)

代码：

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

public class FileCopyExample {
    public static void copyFile(String sourcePath, String destinationPath, String newFileName) throws IOException {
        // 创建目标目录
        File directory = new File(destinationPath);
        if (!directory.exists()) {
            directory.mkdir();
        }

        // 构建源文件和目标文件路径
        File sourceFile = new File(sourcePath);
        File destinationFile = new File(directory.getAbsolutePath() + File.separator + newFileName);

        // 复制文件
        Path source = sourceFile.toPath();
        Path destination = destinationFile.toPath();
        Files.copy(source, destination, StandardCopyOption.REPLACE_EXISTING);

        System.out.println("文件复制成功！");
    }

    public static void main(String[] args) {
        //原来的文件名
        String sourcePath = "E:\\我是源文件.txt";
        //目标目录
        String destinationPath = "E:\\我是一个目录";
        //目标文件名
        String newFileName = "我是新文件.txt";

        try {
            copyFile(sourcePath, destinationPath, newFileName);
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("文件复制失败！");
        }
    }
}
```

**运行结果：**


![img](https://img-blog.csdnimg.cn/img_convert/6267e5f6a59d065cdf748f90030e1a98.png)

这就是一个基础的io流的应用，读者可以自己运行一下试试，其中源文件名，目标目录和目标文件名都可以自定义。这个例子中的方法将会在后面的章节中讲到。

那么，我们开始吧。

## 1 文件

### 1.1 什么是文件

文件就是用来保存数据的地方，比如excel文件，word文件，mp3文件。可以保存图片，视频，声音等等等

### 1.2 文件流

文件**在程序中**是以流的形式操作的

>流：数据在数据源（文件）和程序（内存）之间的路径

>输入流：数据从数据源（文件）到程序（内存）的路径

>输出流：数据从程序（内存）到数据源（文件）的路径

当然，这里的数据源一般来说是磁盘，但也可以是其他的，比如说可能是来自网络，也有可能是来自数据库。


![img](https://img-blog.csdnimg.cn/img_convert/3de33e244c41c37efdf752920c631ffc.png)

## 2 常见的文件操作

### 2.1 创建文件对象的构造器和方法

#### 2.1.1 相关方法：

>new File(String pathname)/根据路径字符串构建一个File对象<br>
 new File(File parent,String child)/根据父目录文件对象+子路径字符串构建<br>
 new File(String parent,String child)/根据父目录字符串+子路径字符串构建

**注意**，**创建的File对象仅仅表示你正在操作的文件对象的路径**，并不会在系统文件夹中自动创建该文件。如果你想在指定的路径中创建一个文件，可以使用File对象的方法，如file.createNewFile()。通过这个方法，你可以在指定的路径下创建一个空的新文件。但是请注意，**如果指定路径所在的目录不存在，你需要确保先创建这个目录，然后才能成功创建文件。**（后面会讲解创建目录的方法）

#### 2.1.2 构造方法和创建文件方法使用

1 new File(String pathname)/根据路径字符串构建一个File对象

```java
@Test
    public void fileDemo1(){
        //这里创建了一个File对象，但是并没有在你电脑的文件夹里创建文件
        //路径为两个反斜杠'\\'的原因在2.1.3中
        File file=new File("e:\\newfile1.txt");
        try {
            //运行了这个方法后，才正式创建了文件
             file.createNewFile();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
```

运行结果：


![img](https://img-blog.csdnimg.cn/img_convert/40e2ba562b1a68554ae486754c769bc4.png)

2 new File(File parent,String child)/根据父目录文件对象+子路径字符串构建

```java
@Test
    public void fileDemo12(){
        File fileParent=new File("e:\\");
        File file=new File(fileParent,"newFile2.txt");
        try {
             file.createNewFile();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
```

3 new File(String parent,String child)/根据父目录字符串+子路径字符串构建

```java
@Test
    public void fileDemo3(){
        File file=new File("e:\\","newFile3.txt");
        try {
             file.createNewFile();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }
```

#### 2.1.3 小知识：为什么有的路径分隔符是"\\"，有的是"/"

>在windows中，用于表示路径的字符串中，路径分隔符使用的是反斜杠（\）而不是斜杠（/）。这是因为在Windows操作系统中，使用反斜杠作为路径分隔符。而斜杠在Windows操作系统中通常用作命令行参数的前缀，因此不适合作为路径分隔符。

总结：你可以根据个人喜好和代码需求来选择使用斜杠(/)或双反斜杠(\\)作为文件路径分隔符。无论你选择哪个，Java都可以自动处理它们，并在不同的操作系统上正常运行。

### 2.2 获取文件的相关信息

新建File文件后，可以通过File自带的方法获取file的相关信息：

这里我们直接获取上一节中新建的"newFile1.txt"文件的信息

```java
@Test
    public void fileDemo3(){
        File file=new File("e:/","newFile1.txt");
        //调用相应的方法，得到对应信息
        System.out.println("文件名字=" + file.getName());
        System.out.println("文件绝对路径=" + file.getAbsolutePath());
        System.out.println("文件父级目录=" + file.getParent());
        System.out.println("文件大小(字节)=" + file.length());
        System.out.println("文件是否存在=" + file.exists());//T
        System.out.println("是不是一个文件=" + file.isFile());//T
        System.out.println("是不是一个目录=" + file.isDirectory());//F
    }
```

运行结果：

```java
文件名字=newFile1.txt
文件绝对路径=e:\newFile1.txt
文件父级目录=e:\
文件大小(字节)=6
文件是否存在=true
是不是一个文件=true
是不是一个目录=false
```

如果随便设置一个路径，实际上并不存在这个文件或目录File file=new File("e:/","hhhh.txt");：

运行结果：文件不存在，且不是文件也不是目录

```java
文件名字=hhhh.txt
文件绝对路径=e:\hhhh.txt
文件父级目录=e:\
文件大小(字节)=0
文件是否存在=false
是不是一个文件=false
是不是一个目录=false
```

### 2.3 目录的操作和文件删除

><strong>目录创建</strong>

><strong>文件，空目录删除</strong>

以下用三个例子来使用上面的方法

1 判断文件是否存在，存在就删除

```java
//判断文件是否存在，存在就删除
    @Test
    public void fileDelete(){
        File file=new File("e:/newfile1.txt");
        //调用相应的方法，得到对应信息

        System.out.println("文件是否存在=" + file.exists());//T
        if(file.exists()){
            file.delete();
        }
    }
```

执行结束后，文件成功删除

2 判断目录是否存在，存在就删除(**只能删除空白目录**)

```java
@Test
    public void directoryDelete(){
         //由此可见，java把文件夹也看作一个特殊的文件
        File file=new File("e:/newdirectory1");
        //调用相应的方法，得到对应信息
        System.out.println("目录是否存在=" + file.exists());//T
        if(file.exists()){
            file.delete();
        }
```

3 判断目录是否存在，不存在就创建

创建目录有两种方法，当创建多级目录的时候，需要使用mkdirs()方法，若使用mkdir()会创建失败；

只创建一级目录可以使用mkdir()。

比如现在我们的文件夹中存在e:/newdirectory1文件夹，然后我要创建一个e:/newdirectory1/2文件夹就可以使用mkdir()；若要创建e:/newdirectory1/2/3,则只能用mkdirs()

```java
//判断目录是否存在，不存在就创建
    @Test
    public void directoryCreate(){
        File file=new File("e:/newdirectory1/2/3");
        //调用相应的方法，得到对应信息

        System.out.println("目录是否存在=" + file.exists());//T
        if(!file.exists()){
            file.mkdirs();
        }
        System.out.println("目录是否存在=" + file.exists());//T

    }
```

## 3 IO 流原理及流的分类

### 3.1 IO流原理及流的分类

1. **I/O**是**Input/Output**的缩写，I/O技术是非常实用的技术，用于处理数据传输**如读/写文件，网络通讯**等。之后我们在学框架，做项目的时候就会有感受（比如上传下载接口）
2. Java程序中，对于数据的**输入/输出操作以”流(stream)”的方式进行**。
3. java.io包下提供了各种"流"类和接口，用以**获取不同种类的数据**，并通过方法输入或输出数据
4. 输入input:**读取外部数据**(磁盘、光盘等存储设备的数据)**到程序**（内存）**中**。
5. 输出output:将程序（内存）数据**输出**到磁盘、光盘等存储设备中

### 3.2 流的分类

按**操作数据单位**不同分为：**字节流**(8bt)(操作效率稍微低一些，但是处理二进制文件，如音频，视频，可以无损传输)，**字符流**（按字符）文本文件(需要考虑文件编码)
 按**数据流的流向**不同分为：**输入流**，**输出流**
 按**流的角色**的不同分为：**节点流**，**处理流/包装流**


1. Java的IO流共涉及40多个类，实际上非常规则，都是从如上4个抽象基类派生的
2. 由这四个类派生出来的子类名称都是以其父类名作为子类名后缀。

## 4 IO流体系-常用的类

IO流体系图


![img](https://img-blog.csdnimg.cn/img_convert/964319c808c9b84dc561eeae38074054.png)

### 4.1 InputStream 字节输入流·

>InputStream 是所有类字节输入流的超类

常用的子类：

1.**FilelnputStream**: 文件输入流（常用来传输文件）
 2.**BufferedInputStream**: 缓冲字节输入流（带缓冲的流，当然也可以用来传输文件）
 3.**ObjectInputStream**: 对象字节输入流（传输对象的流）

#### 4.1.1 FileInputStream 介绍

**构造器：**

><strong>FileInputStream</strong>(File file)

理解：如果把文件比作快递，内存比作人，快递到人手中需要一个物流（快递），这里的物流就相当于流。构造器就相当于物流系统给我们的文件分配了一个快递员。

##### 实例：

**要求**：使用 FileInputStream 读取 helloworld.txt 文件，并将文件内容显示到控制台.

文件位置及内容：


![img](https://img-blog.csdnimg.cn/img_convert/7f9d3541d4441eec5fa24051931bc86c.png)


```java
@Test
    public void readDocument() {
        FileInputStream fileInputStream=null;
        try {
            //创建FileInputStream对象，用于读取文件
            fileInputStream= new FileInputStream("e:/helloworld.txt");
            int readData = 0;
            //每次读数据会返回下一个字符的值，如果已经到达文件的结尾，返回-1
            while ((readData= fileInputStream.read())!=-1){
                System.out.print((char)readData);
            }
        }  catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                //这个流用完之后一定要记得关闭，因为流也是一种资源，如果不关闭，会造成资源浪费
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```

运行结果：

```java
anddd
111

233
ff
```


但是，如果我们在文件中存放中文，如：


![img](https://img-blog.csdnimg.cn/img_convert/f936eeb8f59131017f96994435d9f4e0.png)

输出的结果就是(乱码)：

```java
æµ‹è¯•ä¸­æ–‡ 
anddd
111

233
ff
```

**原因：**

默认情况下，Java 使用的是 UTF-8 编码格式，而有些文件可能使用其他编码格式，导致读取时出现乱码。

要解决这个问题，可以在读取文件之前指定文件的编码格式，我们可以使用后面要学到的的InputStreamReader类来指定编码格式，来解决这个问题。


我们可以使用InputStream的read(byte[] b)方法来提高传输的效率，之前的read()方法每次只能读取一个字节，而这个方法每次可以读取多个

>read(byte[] b)

**代码**：

```java
@Test
    public void readDocument() {
        FileInputStream fileInputStream=null;
        try {
            //创建FileInputStream对象，用于读取文件
            fileInputStream= new FileInputStream("e:/helloworld.txt");
            //创建一个字节数组，这样我们每次可以读多个字节，本次是每次读8个字节
            byte[] byts=new byte[8];
            //用来存储每次的字节数
            int bytLength=0;
            //如果已经到达文件的结尾，返回-1
            while ((bytLength= fileInputStream.read(byts))!=-1){
                //三个参数分别代表 数组，开始的索引，解码字符的个数
                System.out.print(new String(byts,0,bytLength));
            }
        }  catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```

### 4.2 OutPutStream 字节输出流

#### 4.2.1 FileOutStream

构造方法：

| FileOutputStream(File file)
 创建文件输出流以写入由指定的 File


创建文件输出流以写入由指定的 File
 对象表示的文件。 |
 | FileOutputStream(FileDescriptor fdObj)
 创建文件输出流以写入指定的文件描述符，表示与文件系统中实际文件的现有连接。 |
 | FileOutputStream(String name)
 创建文件输出流以指定的名称写入文件。 |
 | FileOutputStream(String name, boolean append)
 创建文件输出流以指定的名称写入文件。 |

咱们直接通过代码来演示构造方法和一些常用方法

##### 在e盘中的a.txt中写入helloworld

**构造方法1** new FileOutputStream(filePath) 该创建方式写入内容时会覆盖原来的内容

```java
@Test
    public void createTxt() throws IOException {
        String filePath = "e:/a.txt";
        FileOutputStream fileOutputStream = null;
        fileOutputStream = new FileOutputStream(filePath);
        //方法1：写入一个字节
		fileOutputStream.write('a');

        //方法2：写入字符串
        String str = "hello world";
		fileOutputStream.write(str.getBytes());
		
        //方法3：写入字节数组的固定个数 write(byte[] b, int off, int len)
        //从这个字节数组索引为off的字节开始，写入len个字节
        fileOutputStream.write(str.getBytes(), 0, str.length());
    }
```

运行结果：


![img](https://img-blog.csdnimg.cn/img_convert/28bcdf34748c6a4a96fed1f66ec72d15.png)

如果有一起操作的同学会发现两件事情：

1 文件夹里本来没有a.txt，也没有人为创建，文件夹中就自己出现了这个文件

2 代码不管运行几次，文件中的内容都是这些

1是因为使用FileOutputStream 类时，如果指定要写入的文件路径处没有文件，它将自动创建一个新文件进行写入，当然只能有一级文件夹，多级文件夹就不行了

2是因为我们使用的构造方法写入内容时会覆盖原来的内容

**构造方法2** ：FileOutputStream(File file, boolean append)

append - 如果 true ，则字节将被写入文件的末尾而不是开头

我们修改原来代码的构造方法

```java
@Test
    public void createTxt() throws IOException {
        String filePath = "e:/a.txt";
        FileOutputStream fileOutputStream = null;
        fileOutputStream = new FileOutputStream(filePath, true
        );
        //方法1：写入一个字节
        fileOutputStream.write('a');

        //方法2：写入字符串
        String str = "hello world";
        fileOutputStream.write(str.getBytes());

        //方法3：写入字节数组的固定个数 write(byte[] b, int off, int len)
        //从这个字节数组索引为off的字节开始，写入len个字节
        fileOutputStream.write(str.getBytes(), 0, str.length());
    }
```

结果：

可以看到，字节被写到了文件的末尾


![img](https://img-blog.csdnimg.cn/img_convert/4eaa51a63c74d8456cb9c1c183007971.png)

### 4.3 复制一个文件

现在我们使用刚刚学到的方法，复制一个文件

我们复制e盘下的一张图片a.png,复制到e:/a/copy.png

```java
@Test
    public void createTxt() throws IOException {
        FileInputStream fileInputStream=new FileInputStream("e:/a.png");
        //如果上级文件夹不存在，创建上级文件夹
        File copyDir=new File("e:/a");
        if(!copyDir.exists()){
            copyDir.mkdirs();
        }
        FileOutputStream fileOutputStream=new FileOutputStream("e:/a/copy.png");
        byte[] bytes=new byte[1024];
        int bytLength=0;
        while ((bytLength=fileInputStream.read(bytes)) != -1){
            //必须要用这个方法，不然可能会出现文件损失
          fileOutputStream.write(bytes,0,bytLength);
        }
        //不要忘了关闭流
        fileOutputStream.close();
        fileInputStream.close();
    }
```

### 4.4 文件字符流



**FileReader和FileWriter是字符流，通过字符来操作io**![img](https://img-blog.csdnimg.cn/img_convert/74b302c8e8285c1c75a9cd4e2202cce0.png)![img](https://img-blog.csdnimg.cn/img_convert/4026a116b7de251b0b2fb3004969ace2.png)**FileReader相关方法：**

- new FileReader(file/string) 通过file类或路径来创建
- read()每次读取单个字符串，返回该字符。如果到文件末尾返回-1；（**因为是字符流，所以如果用的是UTF-8编码，会返回三个字节组成的字符。**）
- read(char[]) 批量读取多个字符到数组，返回读取到的字符数，如果到文件末尾返回-1

相关API：

- new String (char[])
- new String (char[],off,len) **off:偏移量表示要解码的第一个字节的索引，len长度表示要解码的字节数**

**FileWriter相关方法：**

- new FileWriter(File/String):覆盖摸式，相当于流的指针在首端
- new FileWriter(File/String,true):追加模式，相当于流的指针在尾端
- write(int):写入单个字符
- write(char[]):写入指定数组
- write(char[],off,len):写入指定数组的指定部分
- write(string):写入整个字符串
- write(string,off,len):写入字符串的指定部分

相关APl:

- String类：toCharArray:将String转换成char[]

>注意：<br><strong>FileWriter使用后！必须要关闭(close)或刷新(flush),否则写入不到指定的文件！</strong>

**FileReader使用：**

```java
//单个字符串读取
	@Test
    public void print1() throws IOException {
        FileReader fileReader = new FileReader("E:\\ice.txt");
        int readDate = 0;
        while ((readDate = fileReader.read()) != -1) {
            System.out.print((char) readDate);
        }
    }
	//字符数组读取
    @Test
    public void print2() throws IOException {
        FileReader fileReader = new FileReader("E:\\ice.txt");
        int readNum = 0;
        char[] readDate=new char[8];
        while ((readNum = fileReader.read(readDate)) != -1) {
            System.out.print(new String(readDate,0,readNum));
        }
    }
```

FileWriter使用:

```java
@Test
    public void print2() throws IOException {
    	//带上true，代表追加（在原本文本的后面添加下面的字符）
        FileWriter fileWriter=new FileWriter("E:\\ice.txt",true);
		//  write(int):写入单个字符
		fileWriter.write('H');
		//  write(char[]):写入指定数组
		fileWriter.write(chars);
		//  write(char[],off,len):写入指定数组的指定部分
		fileWriter.write("韩顺平教育".toCharArray(), 0, 3);
		//  write（string）：写入整个字符串
		fileWriter.write(" 你好北京~");
		fileWriter.write("风雨之后，定见彩虹");
        fileWriter.flush();

    }
```

## 5 节点流和处理流


![img](https://img-blog.csdnimg.cn/img_convert/ccb2e7af3b89c908a4a59949ccaf592c.png)

**基本介绍：**

- 节点流可以从特定数据源读取数据，如FileReader、FileWriter
- 处理流：是对一个已存在的流的连接和封装，通过所封装的流的功能调用实现数据读写。如BufferedReader。**处理流的构造方法总是要带一个其他的流对象做参数**。一个流对象经过其他流的多次包装，称为流的链接。

**节点流和处理流的区别和联系**

- 节点流是底层流/低级流，直接跟数据源连接。
- 处理流（包装流）包装节点流，既可以消除不同节点流的实现差异，也可以提供更方便的方法来完成输入和输出。
- 处理流对节点流进行包装，使用了**修饰器设计模式**，不会直接与数据源相连接。

>修饰器设计模式：增加一个修饰类包裹原来的类，包裹的方式一般是通过在将原来的对象作为修饰类的构造函数的参数。装饰类实现新的功能，但是，在不需要用到新功能的地方，它可以直接调用原来的类中的方法。修饰类必须和原来的类有相同的接口。

### 5.1 缓冲流

首先我们来认识认识一下缓冲流,也叫高效流，是对4个FileXxx 流的“增强流”。

**缓冲流的基本原理**：

>1、使用了底层流对象从具体设备上获取数据，并将数据存储到缓冲区的数组内。<br>
 2、通过缓冲区的read()方法从缓冲区获取具体的字符数据，这样就提高了效率。<br>
 3、如果用read方法读取字符数据，并存储到另一个容器中，直到读取到了换行符时，将另一个容器临时存储的数据转成字符串返回，就形成了readLine()功能。

也就是说在创建流对象时，会创建一个内置的默认大小的缓冲区数组，通过缓冲区读写，减少系统IO次数，从而提高读写的效率。

缓冲书写格式为BufferedXxx，按照数据类型分类：

- **字节缓冲流**：BufferedInputStream，BufferedOutputStream
- **字符缓冲流**：BufferedReader，BufferedWriter

#### 5.1.1 字节缓冲流

**构造方法**

- public BufferedInputStream(InputStream in) ：创建一个新的缓冲输入流，注意参数类型为**InputStream**。
- public BufferedOutputStream(OutputStream out)： 创建一个新的缓冲输出流，注意参数类型为**OutputStream**。

缓冲流读写的方式和节点流基本上是一致的，不过效率会大大提高

```java
public class BufferedDemo {
    public static void main(String[] args) throws FileNotFoundException {
        // 记录开始时间
      	long start = System.currentTimeMillis();
		// 创建流对象
        try (
         BufferedInputStream bis = new BufferedInputStream(new FileInputStream("e:\\ice.exe"));
	     BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("e:\\copyPy.exe"));
        ){
        // 读写数据
            int b;
            while ((b = bis.read()) != -1) {
                bos.write(b);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
		// 记录结束时间
        long end = System.currentTimeMillis();
        System.out.println("缓冲流复制时间:"+(end - start)+" 毫秒");
    }
}

缓冲流复制时间:8016 毫秒
```

```java
public class BufferedDemo {
    public static void main(String[] args) throws FileNotFoundException {
      	// 记录开始时间
        long start = System.currentTimeMillis();
		// 创建流对象
        try (
		 BufferedInputStream bis = new BufferedInputStream(new FileInputStream("e:\\ice.exe"));
		 BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("e:\\copyPy.exe"));
        ){
          	// 读写数据
            int len;
            byte[] bytes = new byte[8*1024];
            while ((len = bis.read(bytes)) != -1) {
                bos.write(bytes, 0 , len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
		// 记录结束时间
        long end = System.currentTimeMillis();
        System.out.println("缓冲流使用数组复制时间:"+(end - start)+" 毫秒");
    }
}
缓冲流使用数组复制时间:521 毫秒
```

#### 5.1.2 字符缓冲流

**构造方法**
 相同的来看看其构造，其格式以及原理和字节缓冲流是一样一样的！

- public BufferedReader(Reader in) ：创建一个新的缓冲输入流，注意参数类型为**Reader**。
- public BufferedWriter(Writer out)： 创建一个新的缓冲输出流，注意参数类型为**Writer**。

**字符缓冲流特有方法**
 字符缓冲流的基本方法与普通字符流调用方式一致，这里不再阐述，我们来看字符缓冲流具备的**特有**方法。

- BufferedReader：public String readLine(): **读一行数据**。 **读取到最后返回null**
- BufferedWriter：public void newLine(): **换行**,由系统属性定义符号。

readLine方法演示代码如下：、

```java
public class BufferedReaderDemo {
    public static void main(String[] args) throws IOException {
      	 // 创建流对象
        BufferedReader br = new BufferedReader(new FileReader("e:\\ice.txt"));
		// 定义字符串,保存读取的一行文字
        String line  = null;
      	// 循环读取,读取到最后返回null
        while ((line = br.readLine())!=null) {
            System.out.print(line);
            System.out.println();
        }
		// 释放资源
        br.close();
    }
}
```

newLine方法演示代码如下：

```java
public class BufferedWriterDemo throws IOException {
  public static void main(String[] args) throws IOException  {
    	// 创建流对象
  	BufferedWriter bw = new BufferedWriter(new FileWriter("e:\\ice.txt"));
    	// 写出数据
      bw.write("你好");
    	// 写出换行
      bw.newLine();
      bw.write("好久");
      bw.newLine();
      bw.write("不见");
      bw.newLine();
      bw.write("甚是想念？");
      bw.newLine();
  	// 释放资源
      bw.close();
  }
}
输出效果:
你好
好久
不见
甚是想念？
```

### 5.2 转换流


![img](https://img-blog.csdnimg.cn/img_convert/c6771456fcd229d81436e446119f8a83.png)

#### 5.2.1 字符编码和解码

电脑中存放的所有数据，包括图片，音视频，文字，都是以二进制的形式存放的。而我们在屏幕上看到的文字，标点，都是二进制解析出来的。这种将二进制数据通过某种规则转化成字符的过程，叫做**解码**。而将按照某种规则，将字符存储到计算机中，称为**编码**。

简单一点的说就是：

>编码:字符(能看懂的)–字节(看不懂的）<br>
 解码:字节(看不懂的)–&gt;字符(能看懂的)

- **字符编码** Character Encoding: 就是一套自然语言的字符与二进制数之间的对应规则。
- **字符集 **Charset：也叫编码表。是一个系统支持的所有字符的集合，包括各国家文字、标点符号、图形符号、数字等。


计算机要准确的存储和识别各种字符集符号，需要进行字符编码，一套字符集必然至少有一套字符编码。常见字符集有ASCII字符集、GBK字符集、Unicode字符集等。![img](https://img-blog.csdnimg.cn/img_convert/eb7ce47b207fba824239024f4885e86c.png)

#### 5.2.2 编码问题导致乱码

在java开发工具IDEA中，使用FileReader 读取项目中的文本文件。由于IDEA的设置，都是默认的UTF-8编码，所以没有任何问题。但是，当读取到GBK编码的文本文件时，就会出现乱码。

```java
public class ReaderDemo {
    public static void main(String[] args) throws IOException {
        FileReader fileReader = new FileReader("C:\\a.txt");
        int read;
        while ((read = fileReader.read()) != -1) {
            System.out.print((char)read);
        }
        fileReader.close();
    }
}
输出结果：���
```

那么如何读取GBK编码的文件呢？ 这个时候就得讲讲转换流了！

#### 5.2.3 InputStreamReader-字节流转换成字符流

Reader的子类，可以将**InputStream(字节流)转换成Reader(字符流)**

**构造代码：**

><strong>InputStreamReader isr = new InputStreamReader(new FileInputStream(“in.txt”));</strong><br><strong>InputStreamReader isr2 = new InputStreamReader(new FileInputStream(“in.txt”) , “GBK”);</strong>

```java
public static void main(String[] args) throws IOException {
   	// 定义文件路径,文件为gbk编码
     String FileName = "C:\\A.txt";
   	// 创建流对象,默认UTF8编码
     InputStreamReader isr = new InputStreamReader(new FileInputStream(FileName));
   	// 创建流对象,指定GBK编码
     InputStreamReader isr2 = new InputStreamReader(new FileInputStream(FileName) , "GBK");
	// 定义变量,保存字符
     int read;
   	// 使用默认编码字符流读取,乱码
     while ((read = isr.read()) != -1) {
         System.out.print((char)read); // �����ʺ      
     }
     isr.close();
   
   	// 使用指定编码字符流读取,正常解析
     while ((read = isr2.read()) != -1) {
         System.out.print((char)read);// 姐就是女王
     }
     isr2.close();
 }
```

#### 5.2.4 OutputStreamWriter-字符流转换为字节流

Writer的子类，它的作用是将字符流转换为字节流，使得字符流可以以指定格式被写入到输出流中。
 构造方法：

>OutputStreamWriter isr = new OutputStreamWriter(new FileOutputStream(“a.txt”));<br>
 OutputStreamWriter isr2 = new OutputStreamWriter(new FileOutputStream(“b.txt”) , “GBK”);

```java
public static void main(String[] args) throws IOException {
        String text = "Hello, world!";
        FileOutputStream fos = new FileOutputStream("output.txt");
        OutputStreamWriter osw = new OutputStreamWriter(fos, "UTF-8");
        osw.write(text);
        osw.close();
    }
```

### 5.3 对象流（序列化流）

#### 详细介绍序列化流

序列化流是一种将对象转换为字节流的过程，以便可以将对象保存到磁盘上，将其传输到网络上，或者将其存储在内存中，以后再进行反序列化，将字节流重新转换为对象。序列化流的作用是实现对象的持久化和跨平台传输。

要使用序列化流，需要**满足以下条件**：

- 对象所属的类必须实现 java.io.Serializable 接口，这是一个标记接口，没有任何方法，只是用于标识类可以被序列化。
- 对象的所有属性必须是可序列化的，如果有一个属性不是可序列化的，则该属性必须用 transient 关键字修饰，表示该属性不参与序列化。
- 对象所属的类最好提供一个 serialVersionUID 字段，这是一个长整型常量，用于标识类的版本号，如果没有提供，系统会自动生成一个，但是可能会因为类的修改而变化，导致反序列化失败。

序列化流的使用步骤如下：

- 创建一个 ObjectOutputStream 对象，构造方法的参数是一个 OutputStream 对象，可以是任意的字节输出流，如 FileOutputStream。
- 调用 ObjectOutputStream 的 writeObject 方法，传入要序列化的对象，该方法会将对象转换为字节流，并写入到指定的输出流中。
- 关闭 ObjectOutputStream 对象，释放资源。

反序列化流是一种将字节流转换为对象的过程，它是序列化流的逆过程。反序列化流的作用是从文件或网络中读取对象，以便在程序中使用。

反序列化流的使用步骤如下：

- 创建一个 ObjectInputStream 对象，构造方法的参数是一个 InputStream 对象，可以是任意的字节输入流，如 FileInputStream。
- 调用 ObjectInputStream 的 readObject 方法，该方法会从指定的输入流中读取字节流，并将其转换为对象，返回值是一个 Object 对象，需要强制类型转换为原来的对象类型。
- 关闭 ObjectInputStream 对象，释放资源。

以下是一个使用序列化流和反序列化流的示例，其中定义了一个 Person 类，实现了 Serializable 接口，并提供了一个 serialVersionUID 字段。然后创建了一个 Person 对象，并使用 ObjectOutputStream 将其序列化到一个文件中，再使用 ObjectInputStream 从文件中反序列化该对象

```java
import java.io.*;

// 定义一个 Person 类，实现 Serializable 接口
class Person implements Serializable {
    // 提供一个 serialVersionUID 字段，标识类的版本号
    private static final long serialVersionUID = 1L;
    // 定义两个属性，name 和 age
    private String name;
    private int age;

    // 提供构造方法，设置属性的值
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 提供 toString 方法，返回对象的信息
    public String toString() {
        return "Person{name=" + name + ", age=" + age + "}";
    }
}

public class Demo {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        // 创建一个 Person 对象
        Person p = new Person("张三", 18);
        // 创建一个 ObjectOutputStream 对象，传入一个 FileOutputStream 对象，指定文件名为 person.txt
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.txt"));
        // 调用 writeObject 方法，将 Person 对象序列化到文件中
        oos.writeObject(p);
        // 关闭 ObjectOutputStream 对象
        oos.close();

        // 创建一个 ObjectInputStream 对象，传入一个 FileInputStream 对象，指定文件名为 person.txt
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.txt"));
        // 调用 readObject 方法，从文件中反序列化 Person 对象，需要强制类型转换
        Person p2 = (Person) ois.readObject();
        // 关闭 ObjectInputStream 对象
        ois.close();
        // 打印反序列化得到的对象
        System.out.println(p2);
    }
}
```

运行结果是：

```java
Person{name=张三, age=18}
```

说明序列化流和反序列化流成功地将对象保存到文件中，并从文件中读取对象。这就是序列化流和反序列化流的基本用法。

#### 一些问题

**为什么要进行序列化的工作，有哪些场景需要进行序列化**
 一般来说，有以下几种场景需要进行序列化：

- 当你想把内存中的对象保存到文件中，以便在其他时间或其他地方重新加载和使用，例如保存游戏进度，保存用户设置，保存用户数据等。
- 当你想把对象通过网络传输给其他程序或其他机器，以便在远程进行处理或展示，例如远程方法调用，分布式计算，网络通信等。
- 当你想把对象存储在内存中，以便在不同的线程或不同的模块之间共享或传递，例如消息队列，缓存系统，事件驱动等。

**当你想把对象通过网络传输给其他程序或其他机器，以便在远程进行处理或展示，例如远程方法调用，分布式计算，网络通信等。 这一条不是很懂，可以说详细一些吗。比如我调用一个接口，调用接收的类需要序列化吗。**
 好的，我来解释一下这一条的意思。当你想把对象通过网络传输给其他程序或其他机器，就是说你想把一个Java对象从一个JVM（Java虚拟机）发送到另一个JVM，这样你就可以在不同的机器上运行不同的Java程序，但是它们之间可以相互通信和协作。例如，你可以把一个对象发送到一个服务器上，让服务器对这个对象进行一些复杂的计算或处理，然后把结果返回给你，这就是远程方法调用（RMI）的一个应用场景。或者，你可以把一个对象发送到一个客户端上，让客户端显示这个对象的内容或状态，这就是网络通信的一个应用场景。
 但是，要实现这样的功能，你需要对对象进行序列化和反序列化。序列化就是把对象转换成字节流的过程，反序列化就是把字节流还原成对象的过程。这样，你才能把对象通过网络发送和接收，因为网络只能传输字节数据。所以，如果你想把对象通过网络传输给其他程序或其他机器，你就需要对对象进行序列化和反序列化。
 你提到的调用一个接口的问题，其实就是RMI的一个例子。如果你调用的接口是一个远程接口，也就是说，这个接口的实现类是在另一个JVM中运行的，那么你就需要对调用的参数和返回值进行序列化和反序列化，因为这些参数和返回值都是对象，它们需要通过网络传输。如果你调用的接口是一个本地接口，也就是说，这个接口的实现类是在同一个JVM中运行的，那么你就不需要对调用的参数和返回值进行序列化和反序列化，因为这些参数和返回值都是在内存中直接传递的，不需要通过网络。
 希望这样能让你更清楚地理解这一条的意思。如果你还有其他问题，欢迎继续提问。😊

**可是我调用远程接口的时候，并没有将我的类进行序列化，照样可以介绍到对面返回的数据：**
 你调用远程接口的时候，可能是使用了一些框架或库，它们已经帮你实现了序列化和反序列化的功能，所以你不需要自己去做。例如，如果你使用的是 Java RMI（Remote Method Invocation）框架，它会自动为你处理对象的序列化和反序列化，你只需要关注业务逻辑。或者，如果你使用的是 JSON（JavaScript Object Notation）格式，它是一种常用的数据交换格式，它可以将对象转换为字符串，或者将字符串转换为对象，你可以使用一些库，如 Gson 或 Jackson，来实现对象和 JSON 字符串之间的转换，这也是一种序列化和反序列化的过程。
 所以，你调用远程接口的时候，并没有将你的类进行序列化，并不是说序列化和反序列化不需要，而是说它们已经被封装在了其他的工具中，你不需要直接操作它们。但是，如果你想了解它们的原理和细节，你还是需要学习序列化流和反序列化流的知识的。😊**所以我使用的框架是springboot，我在调用接口的时候，实际上传输的是json是吗。为什么我的类转化为json，就属于序列化了呢：**
 是的，你使用的框架是springboot，你在调用接口的时候，实际上传输的是json。json是一种数据交换格式，它可以将对象转换为字符串，或者将字符串转换为对象。这样，你就可以把对象通过网络发送和接收，因为网络只能传输字节数据。这个过程就属于序列化和反序列化。
 为什么你的类转化为json，就属于序列化了呢？因为序列化的本质就是把对象的状态（属性的值）保存到一个可存储或可传输的媒介中，例如文件，内存，网络等。json就是一种可存储或可传输的媒介，它是一种文本格式，可以用文件或字节流来保存或传输。当你把你的类转化为json时，你就是把你的类的状态保存到了一个json字符串中，这就是序列化。当你把json字符串转化为你的类时，你就是把json字符串中的状态还原到了你的类中，这就是反序列化。所以，你的类转化为json，就属于序列化了。😊

**那为什么我还要实现java.io.Serializable呢，我不是已经转换为json了吗**
 你不一定要实现java.io.Serializable接口，这取决于你使用的是哪种序列化和反序列化的方式。如果你使用的是json格式，那么你可以使用一些库，如Gson或Jackson，来实现对象和json字符串之间的转换，这些库不需要你的类实现java.io.Serializable接口，它们只需要你的类有一个无参的构造方法，和一些公开的或者有注解的属性或方法，就可以自动地将你的类转化为json，或者将json转化为你的类。但是，如果你使用的是Java自带的序列化和反序列化的方式，也就是使用ObjectOutputStream和ObjectInputStream，那么你就必须让你的类实现java.io.Serializable接口，这是一个标记接口，没有任何方法，只是用于标识类可以被序列化。如果你的类没有实现这个接口，而你试图用ObjectOutputStream或ObjectInputStream对它进行序列化或反序列化，那么你就会抛出一个NotSerializableException异常，表示你的类不可序列化。
 所以，你是否要实现java.io.Serializable接口，要看你使用的是哪种序列化和反序列化的方式，不同的方式有不同的要求。你可以根据你的需求和喜好，选择合适的方式。😊

**那我怎么知道我使用的是哪种序列化方式呢。或者说，哪些时候是json，哪些时候用ObjectOutputStream和ObjectInputStream呢**
 至于哪些时候是json，哪些时候用ObjectOutputStream和ObjectInputStream，这没有一个固定的答案，这取决于你的需求和喜好，不同的方式有不同的优缺点。一般来说，json格式比较简单，通用，易读，易传输，可以和其他语言的程序进行交互，但是它不能保存对象的所有信息，例如类的元数据，方法，静态属性等，而且它的转换效率可能不如Java自带的方式高。Java自带的方式比较复杂，专用，不易读，不易传输，只能和Java语言的程序进行交互，但是它可以保存对象的所有信息，而且它的转换效率可能比json格式高。所以，你需要根据你的具体情况，选择合适的方式。😊

**我要使用hutool的网络工具，调用某个api平台的一个post接口，在这种场景应该如何写代码，这个时候需要进行序列化和反序列化吗**
 你可以使用hutool的网络工具，调用某个api平台的一个post接口，具体的代码如下：

```java
// 引入hutool的http模块
import cn.hutool.http.HttpUtil;

// 创建一个HashMap对象，用于存放请求参数
HashMap<String, Object> paramMap = new HashMap<>();
// 添加请求参数，根据具体的api平台的要求，可能需要添加一些认证信息，例如appKey，appSecret等
paramMap.put("param1", "value1");
paramMap.put("param2", "value2");

// 调用HttpUtil的post方法，传入api平台的url和请求参数，返回一个字符串，表示响应的内容
String result = HttpUtil.post("https://api.example.com/post", paramMap);

// 打印响应的内容
System.out.println(result);
```

这种场景下，你不需要进行序列化和反序列化，因为hutool的http模块已经帮你实现了这些功能。你只需要传入一个Map对象，hutool会自动将它转换为表单格式或者json格式，根据你的请求头的Content-Type的值。同样，你也不需要解析响应的内容，hutool会自动将它转换为字符串，你可以直接使用。当然，如果你想对响应的内容进行更多的处理，你可以使用hutool的json模块，将字符串转换为json对象，然后进行操作。

**hutool哪里帮我序列化了，我咋没看到**
 hutool在HttpUtil的post方法中帮你序列化了，你可能没有注意到。如果你看一下HttpUtil的源码，你会发现，当你传入一个Map对象作为请求参数时，hutool会根据你的请求头的Content-Type的值，来决定将Map对象转换为什么格式的数据。如果你的Content-Type是application/x-www-form-urlencoded，那么hutool会将Map对象转换为表单格式的数据，也就是key=value&amp;key=value的形式。如果你的Content-Type是application/json，那么hutool会将Map对象转换为json格式的数据，也就是{“key”:“value”,“key”:“value”}的形式。这些转换的过程，其实就是序列化的过程，只不过hutool已经封装好了，你不需要自己去写。😊

### 5.4 打印流

实际上，我们平常使用的System.out.println就是打印流**打印流分类：**

>字节打印流PrintStream，字符打印流PrintWriter

**打印流特点：**

>A:**只操作目的地,不操作数据源 **<br>
 B:可以操作任意类型的数据<br>
 C:如果启用了自动刷新，在调用println()方法的时候，能够换行并刷新<br>
 D:可以直接操作文件

```java
public static void main(String[] args) throws IOException {
        BufferedReader br=new BufferedReader(new FileReader("e:\\ice.txt"));
        PrintStream ps=new PrintStream("e:\\printcopy.txt");
        String line;
        while((line=br.readLine())!=null) {
            ps.println(line);
        }
        br.close();
        ps.close();
    }
```

```java
public static void main(String[] args) throws IOException {
        BufferedReader br=new BufferedReader(new FileReader("aa.txt"));
        PrintWriter pw=new PrintWriter("printcopyaa.txt");
        String line;
        while((line=br.readLine())!=null) {
            pw.println(line);
        }
        br.close();
        pw.close();
    }
```

### 5.4 Properties

**构造方法**
 public Properties() :创建一个空的属性列表。**基本的存储方法**
 public Object setProperty(String key, String value) ： 保存一对属性。
 public String getProperty(String key) ：使用此属性列表中指定的键搜索属性值。
 public Set stringPropertyNames() ：所有键的名称的集合。

```java
public class ProDemo {
    public static void main(String[] args) throws FileNotFoundException {
        // 创建属性集对象
        Properties properties = new Properties();
        // 添加键值对元素
        properties.setProperty("filename", "a.txt");
        properties.setProperty("length", "209385038");
        properties.setProperty("location", "D:\\a.txt");
        // 打印属性集对象
        System.out.println(properties);
        // 通过键,获取属性值
        System.out.println(properties.getProperty("filename"));
        System.out.println(properties.getProperty("length"));
        System.out.println(properties.getProperty("location"));

        // 遍历属性集,获取所有键的集合
        Set<String> strings = properties.stringPropertyNames();
        // 打印键值对
        for (String key : strings ) {
            System.out.println(key+" -- "+properties.getProperty(key));
        }
    }
}
输出结果：
{filename=a.txt, length=209385038, location=D:\a.txt}
a.txt
209385038
D:\a.txt
filename -- a.txt
length -- 209385038
location -- D:\a.txt
```

**与流相关的方法**
 public void load(InputStream inStream)： 从字节输入流中读取键值对。
 参数中使用了字节输入流，通过流对象，可以关联到某文件上，这样就能够加载文本中的数据了。现在文本数据格式如下:

```java
ilename=Properties.txt
length=123
location=C:\Properties.txt
```

**加载代码演示：**

```java
复制代码public class ProDemo {
    public static void main(String[] args) throws FileNotFoundException {
        // 创建属性集对象
        Properties pro = new Properties();
        // 加载文本中信息到属性集
        pro.load(new FileInputStream("Properties.txt"));
        // 遍历集合并打印
        Set<String> strings = pro.stringPropertyNames();
        for (String key : strings ) {
            System.out.println(key+" -- "+pro.getProperty(key));
        }
    }
}
输出结果：
filename -- Properties.txt
length -- 123
location -- C:\Properties.txt
```

文本中的数据，必须是键值对形式，可以使用空格、等号、冒号等符号分隔。

