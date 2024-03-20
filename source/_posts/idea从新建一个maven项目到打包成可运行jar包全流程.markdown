---
layout:  post
title:   idea从新建一个maven项目到打包成可运行jar包全流程
date:   2024-01-03 15:22:28
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-java日常
-java开发使用技巧
-intellij-idea
-maven
-jar

---


## 1 创建maven项目




点击new-project![img](https://img-blog.csdnimg.cn/img_convert/704c9673bce6b313687ff1d8a706dc25.png)
 选择左侧的maven Archetype
 修改Name，JDK，Catalog，Archetype（org.apache.maven.archetypes:maven-archetype-webapp）为下图中配置![img](https://img-blog.csdnimg.cn/img_convert/02fe39c93f5a882d62bd9113362419a8.png)
 修改地址（自选），版本号（自选），之后店家create![img](https://img-blog.csdnimg.cn/img_convert/af45dccc7d8fcf029d87919fb0c42a18.png)

## 2 配置maven


在settings中找到下图中maven的位置，并自定义maven包，点击apply![img](https://img-blog.csdnimg.cn/img_convert/81718d7ed06cf9d010b902bf2ee1e37d.png)

## 3 完善项目结构



在src文件夹右击，分别点击New，DIrectory![img](https://img-blog.csdnimg.cn/img_convert/ee3559ccb24b71a018cc31586d7f0207.png)
 把下面四个各选一遍![img](https://img-blog.csdnimg.cn/img_convert/91a3d1948cab604f6d0fa26e3ec8eebd.png)

## 4 编写代码




这里我将我之前的笔记 [自制java工具实现 ctrl+c+c 翻译鼠标选中文本](http://t.csdnimg.cn/uKNQs)的代码放入项目中:
 依赖：![img](https://img-blog.csdnimg.cn/img_convert/d0b4a1bd8c243c2ea9778fac0c0bf89a.png)
 项目结构：![img](https://img-blog.csdnimg.cn/img_convert/ec3df5be3731736e85408676ef6232dd.png)
 运行成功：![img](https://img-blog.csdnimg.cn/img_convert/56c6886e15fb4ed75b6004891366ed3a.png)

## 5 打包成可执行文件



pom中packaging中的war修改成jar![img](https://img-blog.csdnimg.cn/img_convert/08e392e816bb75fe6ac462e9c72ff9ac.png)
 删除pom文件中，默认生成的build![img](https://img-blog.csdnimg.cn/img_convert/96518ff062d85f05ee63081c778e86d4.png)
 粘贴下面的build配置

```java
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-assembly-plugin</artifactId>
      <executions>
        <execution>
          <phase>package</phase>
          <goals>
            <goal>single</goal>
          </goals>
          <configuration>
            <archive>
              <manifest>
                <!--                  填写你的main方法所在的主类-->
                <mainClass>
                  com.ice.CtrlCCTranslate.GlobalKeyListenerExample
                </mainClass>
              </manifest>
            </archive>
            <descriptorRefs>
              <descriptorRef>jar-with-dependencies</descriptorRef>
            </descriptorRefs>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```



点击下面的Terminal，运行mvn clean package![img](https://img-blog.csdnimg.cn/img_convert/861926d45e7ed5550fb3b078f6bb837d.png)
 BUILD SUCCESS![img](https://img-blog.csdnimg.cn/img_convert/f7c80b7775806dc324d37ee47d4623df.png)

## 6 运行可执行文件



到项目下的target文件夹中找到文件名长的那个jar包，双击运行![img](https://img-blog.csdnimg.cn/img_convert/f6e2d0f37782ec132e110daa1f38802e.png)
 运行成功：![img](https://img-blog.csdnimg.cn/img_convert/a4b2842465553872e0f8924468325664.png)

