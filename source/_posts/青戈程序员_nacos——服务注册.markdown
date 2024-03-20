---
layout:  post
title:   青戈程序员_nacos——服务注册
date:   2022-09-21 08:25:14
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-微服务
-java
-spring boot
-微服务

---


传统大并发，高流量的场景不适合使用普通的技术，所以有了微服务

链接：【最适合小白学习的SpringCloud微服务实战-全程敲代码纯干货分享】https://www.bilibili.com/video/BV1UG411u7XP?vd_source=10e3dfac95ac3a6883b1f8a6c3bc65d5

nacos是springcloud的一个注册中心




#### 1 组件下载


![img](https://img-blog.csdnimg.cn/img_convert/1c4b7901d1fbb73c24f7ae571c1599c8.png)


![img](https://img-blog.csdnimg.cn/img_convert/bdf80580b779707728eede6531b6caae.png)

下载zip

#### 2 创建服务

##### 创建新项目


![img](https://img-blog.csdnimg.cn/img_convert/3f553190af975cff1e9701a72ab4d457.png)

##### 选择组件（暂时选这个，之后再选其他的）


![img](https://img-blog.csdnimg.cn/img_convert/2a1d404aca9a5f50c92c91d33b3889e5.png)

现在这个项目是作为父级，咱们可以把不必要的东西删掉


![img](https://img-blog.csdnimg.cn/img_convert/6222157a6a4c304b380d313953dea864.png)

##### pom：add as maven project


![img](https://img-blog.csdnimg.cn/img_convert/0aa694cb7f96787ac506f304f14dac04.png)

test和start不需要可以删掉


![img](https://img-blog.csdnimg.cn/img_convert/f78bf040bbf15cac394f9c7e85a652ba.png)

父级的作用就是控制版本，版本之间的对应关系一定要对，具体的对应关系可以在springcloudalibaba的GitHub/wiki中找到


![img](https://img-blog.csdnimg.cn/0fd013119c294fb29248fe289f027f89.png#pic_center)

ps：

##### 报错：Cannot resolve plugin org.springframework.boot:spring-boot-maven-plugin:2.7.3

```java
Cannot resolve plugin org.springframework.boot:spring-boot-maven-plugin:2.7.3
```

因为springboot版本要和你的版本一样，解决方法：

 [(4条消息) Cannot resolve plugin org.springframework.boot:spring-boot-maven-plugin: 解决办法_大王我亲自来巡山的博客-CSDN博客](https://blog.csdn.net/weixin_43923436/article/details/121394457)

我将我的版本改成了和自己一样的2.5.2


![img](https://img-blog.csdnimg.cn/img_convert/e1c5aeb218e7379c869a9929f62352dd.png)

#### 3 nacos的启动

nacos的bin文件夹中：cmd是Windows的启动脚本


![img](https://img-blog.csdnimg.cn/667e0bd6489c4ced8e2e2886e1f468f9.png#pic_center)

如果启动不成功，编辑模式打开cmd文件（就是用记事本或者其他软件打开）

找到：set MODE="cluster"

将cluster修改为standalone

==注：==好习惯：添加注释：rem cluster

##### 运行成功画面：


![img](https://img-blog.csdnimg.cn/img_convert/f4d5967e94ed15dcf9764c8fcdd04592.png)

##### 浏览器访问

访问这里的地址，访问成功了说明项目启动成功了：


![img](https://img-blog.csdnimg.cn/img_convert/e6fbea4a6fa8a6cea6bc866dab01c95c.png)


成功：![img](https://img-blog.csdnimg.cn/img_convert/2b0a212115ae82571f8671ac381bb7a8.png)

然后现在访问localhost:8848/nacos

**访问成功**


![img](https://img-blog.csdnimg.cn/img_convert/81a8cf5614e3345f1ed2a2dec2f24ba7.png)

默认的账号密码都是nacos

#### 4 创建子模块

使用maven新建子模块


![img](https://img-blog.csdnimg.cn/img_convert/cf638a3499cf847a336bd43cbf80171a.png)


![img](https://img-blog.csdnimg.cn/img_convert/0be666ddffe35b6d9618527452ca905b.png)

#### 父级pom添加依赖管理

<dependencyManagement>的左右是在父级添加过依赖后，子模块就不用再添加了

这里对应的springboot的版本是2.4.2

```java
<dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>2020.0.1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2021.1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

#### 5 子模块添加nacos依赖


![img](https://img-blog.csdnimg.cn/a80567529fe34601bd85364fd1536abe.png#pic_center)

在模块的pom中添加


![img](https://img-blog.csdnimg.cn/802cb3aec070483e8247d3e213a93551.png#pic_center)

```java
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
</dependency>
```

#### 6 新建启动类


![img](https://img-blog.csdnimg.cn/8f94fc1483584b198d2a225057380f02.png#pic_center)

发现无法添加注解：要在子模块加一个依赖包：web组件

```java
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

实体类：

```java
@SpringBootApplication
public class OrderApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderApplication.class, args);
    }

}
```

#### 7 启动启动类

报错：

```java
java.lang.IllegalArgumentException: Param 'serviceName' is illegal, serviceName is blank
```

原因是什么什么识别不了，要在父级添加一个依赖

```java
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bootstrap</artifactId>
</dependency>
```

虽然引用了nacos，但是没有注册，在启动类添加注解：

```java
@EnableDiscoveryClient
```

#### 8 添加配置

resource中添加配置文件bootstrap.yml

```java
server:
  port: 8000

spring:
  application:
    name: service-order
  cloud:
    nacos:
      server-addr: localhost:8848
      discovery:
        ephemeral: false #如果这里是一个短暂的实例,就用TRUE
```

#### 9 运行

看到nacos registry, DEFAULT_GROUP service-order 2.0.0.1:8000 register finished

说明注册成功

打开nacos查看，发现也注册好了


![img](https://img-blog.csdnimg.cn/2ae100fd77f3443488086c826983e8c9.png#pic_center)

#### 10 多个运行

##### 新建一个运行：

设置端口号和允许并发运行


![img](https://img-blog.csdnimg.cn/71a6cfe454bc4ca0918644751957672b.png#pic_center)

##### 设置多个并发运行：


![img](https://img-blog.csdnimg.cn/7601a0150ac64fc4ab9f60b8d144a237.png#pic_center)

添加springboot


![img](https://img-blog.csdnimg.cn/b2ab712e6a394240b169dfe4d5a48fe8.png#pic_center)

就能看到了：


![img](https://img-blog.csdnimg.cn/f6e01d27b6af4e29af68a20592d8a4e8.png#pic_center)

三个都运行后：


![img](https://img-blog.csdnimg.cn/a278e4cefca94ba7af73826d878a1022.png#pic_center)

