---
layout:  post
title:   java重新开始2 尚硅谷最新SSM教程逐P笔记 1_Mybatis部分
date:   2023-05-31 15:39:25
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-mybatis
-java
-开发语言

---


网址：【【尚硅谷】SSM框架全套教程，MyBatis+Spring+SpringMVC+SSM整合一套通关】https://www.bilibili.com/video/BV1Ya411S7aT?p=4&amp;vd_source=10e3dfac95ac3a6883b1f8a6c3bc65d5

 [最近看视频学习的感悟](http://t.csdn.cn/gZTsL) [JAVA重新开始](http://t.csdn.cn/x2EqR)

这个笔记是我根据视频的P数来记的，把一些网上随时可以搜到的（比如mybatis历史之类的）部分删减，记录下了自己觉得较为重要的知识点,同时还记录了老师在课上讲的，但是可能并没有在官方给的笔记里展现出来的东西。

## p1 课程介绍

先讲mybatis然后讲spring和springmvc

## p2 mybatis历史

mybatis以前是abatis

mybatis是优秀的持久层框架

## p3 mybatis特性

避免了几乎所有手动获得结果集和手动配置参数（自动把sql查询到的结果集解析成java对象）

## p4 mybatis下载

访问网站https://github.com/mybatis/mybatis-3

这是mybatis的GitHub网址，直接下载最新版

## p5 mybatis和其他持久层技术的区别

jdbc：耦合度高（sql是写死的），开发效率低，维护成本高

hibernate：简单了解

mybatis：轻量级，sql和java分开，sql专注数据，java专注业务

## p6 搭建mybatis开发环境

IDE:idea 2019.2
 构建工具：maven3.5.4
 MySQL版本：MySQL8
 MyBatis版本：MyBatis3.5.7

1新建一个空项目

我：D:12_idea/newjava/SSM

2 配置本地maven，配置文件和仓库

3 新建module 选择maven

其中src中的java放的是主程序，resources中放的是配置文件，test中的Java放的是测试程序

module名：mybatis_helloworld

groupid:com.ice

version:1.0

4 在pom.xml中，version下再添加一个打包方式：jar

```java
<groupId>com.ice</groupId>
    <artifactId>mybatis_hellloworld</artifactId>
    <version>1.0</version>
    <packaging>jar</packaging>
```

5 导入一些依赖

```java
<dependencies>
        <!-- Mybatis核心 -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.7</version>
        </dependency>
        <!-- junit测试 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <!-- MySQL驱动 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.16</version>
        </dependency>
    </dependencies>
```

注：如果要使用MySQL5，就要使用5版本的驱动

6 新建数据库 ssm

新建表

```java
CREATE TABLE `t_user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(20) DEFAULT NULL,
  `password` varchar(32) DEFAULT NULL,
  `age` int(11) DEFAULT NULL,
  `gender` varchar(255) DEFAULT NULL,
  `email` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;
```

7 新建对应的实体类

在java文件夹下新建com.ice.mybatis.pojo.User(前面几个是包路径，最后一个是类名)

alt+insert创建有参和无参构造和getset等（或者使用lombok的@Date）

```java
public class User {

    private Integer id;

    private String username;

    private String password;

    private Integer age;



    private String gender;

    private String email;
    public User(){

    }

    public User(Integer id, String username, String password, Integer age, String gender, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.age = age;
        this.gender = gender;
        this.email = email;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", age=" + age +
                ", gender='" + gender + '\'' +
                ", email='" + email + '\'' +
                '}';
    }
```

## p7 创建mybatis核心配置文件

习惯命名为mybatis-config.xml（仅仅是建议，因为整合spring之后是通过文件名来配置的）

核心配置文件主要用来配置连接数据库的环境以及mybatis的全局配置信息

核心配置文件放在src/main/resources下

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--设置连接数据库的环境-->
    <environments default="development">
        <environment id="development">
            <!--事务-->
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/ssm?
serverTimezone=UTC"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <!--引入映射文件-->
    <mappers>
        <mapper resource=""/>
    </mappers>
</configuration>
```

在映射文件中，我们写的才是sql语句,到时候要把映射文件配置在核心配置文件中

## p8 创建mapper接口和映射文件

### 1 mapper

MyBatis中的mapper接口**相当于以前的dao**。但是区别在于，mapper仅仅是接口，我们不需要
 提供实现类。

起名规则，类名+mapper

创建和pojo同级的mapper包

```java
package com.ice.mybatis.mapper;

public interface UserMapper {
    /**
     * 添加用户信息
     */
    int insertUser();
}
```

先写一个添加的方法

### 2 映射文件

在resources中新建一个mappers文件夹，专门用来存放xml文件

新建和UserMapper对应的UserMapper.xml

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.atguigu.mybatis.mapper.UserMapper">
<!--int insertUser();-->
<insert id="insertUser">
insert into t_user values(null,'admin','123456',23,'男','12345@qq.com')
</insert>
</mapper>
```

注意点：

1 namespace 和mapper全类名一致

2 mapper接口中的方法名和映射文件sql语句的id保持一致

**在核心配置文件中配置映射文件**

```java
<mapper resource="mappers/UserMapper.xml"/>
```

## p9 新增测试

### 1 新建测试类

```java
package com.ice.mybatis.test;

import com.ice.mybatis.mapper.UserMapper;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;

public class MyBatisTst {
    @Test
    public void testInsert() throws IOException {
        //输入流
        InputStream is = Resources.getResourceAsStream("mybatis-config.xml");
        //创建SqlSessionFactoryBuilder对象
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new
                SqlSessionFactoryBuilder();
        //通过核心配置文件所对应的字节输入流创建工厂类SqlSessionFactory，生产SqlSession对象
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
        //创建SqlSession对象，此时通过SqlSession对象所操作的sql都必须手动提交或回滚事务
        //SqlSession sqlSession = sqlSessionFactory.openSession();
        //创建SqlSession对象，此时通过SqlSession对象所操作的sql都会自动提交
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        //通过代理模式创建UserMapper接口的代理实现类对象
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        //调用UserMapper接口中的方法，就可以根据UserMapper的全类名匹配元素文件，通过调用的方法名匹配
        int result = userMapper.insertUser();
        System.out.println("结果：" + result);
        sqlSession.commit();
        sqlSession.close();
    }

}
```

1 事务要自己提交，这样才能把数据保留在数据库中

2 创建sqlSession对象时，openSession的参数为true，可以自动提交事务

3 这些代码在之后配置了spring后几乎不用写

4 说实话，这些代码我不怎么看懂

### 2 加入log4j日志功能

1 依赖

```java
<!-- log4j日志 -->
<dependency>
<groupId>log4j</groupId>
<artifactId>log4j</artifactId>
<version>1.2.17</version>
</dependency>
```

2 在resources下加入名为log4j.xml的配置文件

照着复制就行

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
    <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
        <param name="Encoding" value="UTF-8" />
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS}
%m (%F:%L) \n" />
        </layout>
    </appender>
    <logger name="java.sql">
        <level value="debug" />
    </logger>
    <logger name="org.apache.ibatis">
        <level value="info" />
    </logger>
    <root>
        <level value="debug" />
        <appender-ref ref="STDOUT" />
    </root>
</log4j:configuration>
```

之后运行测试类时就会打印一些测试的提示

## p10 优化新增

1. 在创建sqlsession对象时加入参数true，之后就会自动提交事务

## p11 源码验证和日志级别

讲了一下sqlsession获取sql的方法的底层源码

日志级别

FATAL(致命)&gt;ERROR(错误)&gt;WARN(警告)&gt;INFO(信息)&gt;DEBUG(调试)
 从左到右打印的内容越来越详细

## 封装获取sql的代码

新建一个和pojo同级的Utils文件夹，用来存储工具类

新建一个SqlSessionUtil类

```java
package com.ice.mybatis.Utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class SqlSessionUtil {
    public static SqlSession getSqlSession(){
        SqlSession sqlSession=null;
        try {
            InputStream   is = Resources.getResourceAsStream("mybatis-config.xml");
            //创建SqlSessionFactoryBuilder对象
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new
                    SqlSessionFactoryBuilder();
            //通过核心配置文件所对应的字节输入流创建工厂类SqlSessionFactory，生产SqlSession对象
            SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is);
            //创建SqlSession对象，此时通过SqlSession对象所操作的sql都必须手动提交或回滚事务
            //SqlSession sqlSession = sqlSessionFactory.openSession();
            //创建SqlSession对象，此时通过SqlSession对象所操作的sql都会自动提交
            sqlSession = sqlSessionFactory.openSession(true);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return sqlSession;
    }
}
```

之后在测试类中使用

```java
SqlSession sqlSession = SqlSessionUtil.getSqlSession();
```

直接获取sqlSession对象即可

## p12 修改和删除

修改

```java
<!--int updateUser();-->
<update id="updateUser">
update t_user set username='ybc',password='123' where id = 6
</update>
```

删除

```java
<!--int deleteUser();-->
<delete id="deleteUser">
delete from t_user where id = 7
</delete>
```

## p13 查询

### 1 查询实体类对象

```java
<!--User getUserById();-->
<select id="getUserById" resultType="com.atguigu.mybatis.bean.User">
select * from t_user where id = 2
</select>
```

2 查询list集合

```java
<!--List<User> getUserList();-->
<select id="getUserList" resultType="com.atguigu.mybatis.bean.User">
select * from t_user
</select>
```

查询一定要添加resultType或resultMap，resultType就是返回的类的全类名，resultMap之后会讲

resultType：自动映射，用于属性名和表中字段名一致的情况
 resultMap：自定义映射，用于一对多或多对一或字段名和属性名不一致的情况

## p14~p17的核心配置文件的完整文件

后面几p是讲核心配置文件中具体的配置的，在这里先把完好的配置文件放这

```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!--
MyBatis核心配置文件中，标签的顺序：
properties?,settings?,typeAliases?,typeHandlers?,
objectFactory?,objectWrapperFactory?,reflectorFactory?,
plugins?,environments?,databaseIdProvider?,mappers?
-->
<!--引入properties文件-->
<properties resource="jdbc.properties" />
<!--设置类型别名-->
<typeAliases>
<!--
typeAlias：设置某个类型的别名
属性：
type：设置需要设置别名的类型
alias：设置某个类型的别名，若不设置该属性，那么该类型拥有默认的别名，即类名
且不区分大小写
-->
<!--<typeAlias type="com.atguigu.mybatis.pojo.User"></typeAlias>-->
<!--以包为单位，将包下所有的类型设置默认的类型别名，即类名且不区分大小写-->
<package name="com.atguigu.mybatis.pojo"/>
</typeAliases>
<!--
environments：配置多个连接数据库的环境
属性：
default：设置默认使用的环境的id
-->
<environments default="development">
    <!--
environment：配置某个具体的环境
属性：
id：表示连接数据库的环境的唯一标识，不能重复
-->
<environment id="development">
<!--
transactionManager：设置事务管理方式
属性：
type="JDBC|MANAGED"
JDBC：表示当前环境中，执行SQL时，使用的是JDBC中原生的事务管理方式，事
务的提交或回滚需要手动处理
MANAGED：被管理，例如Spring
-->
<transactionManager type="JDBC"/>
<!--
dataSource：配置数据源
属性：
type：设置数据源的类型
type="POOLED|UNPOOLED|JNDI"
POOLED：表示使用数据库连接池缓存数据库连接
UNPOOLED：表示不使用数据库连接池
JNDI：表示使用上下文中的数据源
-->
<dataSource type="POOLED">
<!--设置连接数据库的驱动-->
<property name="driver" value="${jdbc.driver}"/>
<!--设置连接数据库的连接地址-->
<property name="url" value="${jdbc.url}"/>
<!--设置连接数据库的用户名-->
<property name="username" value="${jdbc.username}"/>
<!--设置连接数据库的密码-->
<property name="password" value="${jdbc.password}"/>
</dataSource>
</environment>
    <environment id="test">
<transactionManager type="JDBC"/>
<dataSource type="POOLED">
<property name="driver" value="com.mysql.cj.jdbc.Driver"/>
<property name="url"
value="jdbc:mysql://localhost:3306/ssmserverTimezone=UTC"/>
<property name="username" value="root"/>
<property name="password" value="123456"/>
</dataSource>
</environment>
</environments>
<!--引入映射文件-->
<mappers>
<!--<mapper resource="mappers/UserMapper.xml"/>-->
<!--
以包为单位引入映射文件
要求：
1、mapper接口所在的包要和映射文件所在的包一致
2、mapper接口要和映射文件的名字一致
-->
<package name="com.atguigu.mybatis.mapper"/>
</mappers>
    </configuration>
```

注意，配置文件中各项的顺序是固定的，如果顺序错误就会报错或者运行错误，具体的顺序：

properties?,settings?,typeAliases?,typeHandlers?,
 objectFactory?,objectWrapperFactory?,reflectorFactory?,
 plugins?,environments?,databaseIdProvider?,mappers?

## p14 environment

transactionManager：设置事务管理方式
 属性：
 type=“JDBC|MANAGED”
 JDBC：表示当前环境中，执行SQL时，使用的是JDBC中原生的事务管理方式，事
 务的提交或回滚需要手动处理
 MANAGED：被管理，例如Spring

## p 15 properties

在resources上右键，点击new中的 resource bundle，这个就是properties文件的新建项，本次我们要给jdbc配置一个properties文件，所以name填jdbc

在jdbc.properties文件中填写数据：

```java
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
jdbc.username=root
jdbc.password=1234
```

在核心配置文件中引入properties文件

以后在配置properties文件的时候务必记得在之前加上一个区分的名字（这里的jdbc）

之后我们就可以将核心配置文件中的数据源配置成"${jdbc.driver}"的形式啦（详细看完整配置文件）

## p16 typeAliases 别名

typeAliases 可以给类起别名，之前我们在mapper的xml文件中返回类型写的全类名较长，我们可以在typeAliases 中配置类名的全类名，这样可以省事一点

```java
<typeAliases>
        <typeAlias type="com.ice.mybatis.pojo.User" alias="user"></typeAlias>
    </typeAliases>
```

type属性中写全类名，alias中写别名，这样在mapper的xml文件中就可以直接使用user了

alias也可以不写，如果只写type属性的话，那么别名就默认是类名，且不区分大小写，即在咱们这个例子中，如果不写alias的话，别名就默认是user，或者User也可以（问：那useR呢）

## p17 mappers

除了在mappers中通过<mapper resource="mappers/UserMapper.xml"/>引入具体文件夹以外，我们还可以直接引入一整个文件夹中的xml

当然，因为我们之前说过，mapper中的mapper类和每一个xml是一一对应的，所以为了找到对应的xml文件，在resources中存放xml的文件夹也要和java中mapper的位置一一对应，这里我们在任意一个mapper文件的最上面可以看到包名，我的是com.ice.mybatis.mapper 我们用相同的路径在resources中新建这样路径的文件夹即可

注意，在java中新建的是包，所以可以用com.ice.mybatis.mapper直接新建出对应路径的文件或包，而在resources中默认的是文件夹，如果在文件夹中写com.ice.mybatis.mapper的话，只会 生成一个名为com.ice.mybatis.mapper的文件夹，我们可以新建时填写com/ice/mybatis/mapper，这样就可以生产对应路径的文件夹了，或者，您也可以一层一层新建文件夹，随你

新建完文件夹后，把之前UserMapper.xml文件放到文件夹中，然后将核心配置文件中的mappers下的标签修改为<package name="com.ice.mybatis.mapper"/>

然后再测试测试类中的代码，运行正确

## p18 idea中创建模板

我们不可能每次都去官网复制这些配置，所以我们可以直接将模板放在idea中，以后就可以直接新建了

点击设置-editer-fire and code templates

新增模板

以后右键的时候就可以直接生成模板了

## p19 使用模板新建一个新的模块

没什么讲的，就是建议一些配置文件，如jdbc.properties ;log4j.xml; 等文件可以保存在一个常用文件夹下，以后直接复制就可以

## p20 mybatis获取参数值的两种方式

#{} 占位符的方式

${} 字符串拼接的方式

## p21 mybatis获取参数值的情况（1）

获取个参数值，sql语句中#{}中的参数随便填

## p22 mybatis获取参数值的情况（2）

获取多个参数值，mybatis会默认已arg1 arg2…（或者param1，param2…）为键，参数值为值封装为map集合，所以在sql中填写arg1，arg2就行

## p23 mybatis 获取参数值的情况（3）

既然它默认封装map，那我们也可以封装自己的map来获取参数值呀，

修改UserMapper的方法

User checkLogin(Map&lt;String,Object&gt; map)

之后把数据手动放在map中

## p24 mybatis 获取参数值的情况（4）

参数为对象

## p25 mybatis 获取参数值的情况（5）

@Param

## p26 mybatis的各种查询功能（1）

1 查找一个对象

2 查找多个对象

这节课讲了，查找结果为多个时不可以用对象类型接受，会抛异常

查找单结果时可以用集合接受

## p27 mybatis的各种查询功能（2）

比如要查数据总量

Int findAll();

在sql的返回类型中，我们发现用int,Int ,Integer，integer之类都可以接收，说明mybatis已经帮我们把这些类型的别名配置好了

## p28 mybatis的各种查询功能（3）

查询一条数据，且返回的数据无法和一个已有类对应时，可以直接返回Map

Map&lt;String,Object&gt; findOneById();

在sql的resultType中填写Map就行

## p29 mybatis的各种查询功能（4）

查询一条数据，且返回的数据无法和一个已有类对应时

这下不可以直接用Map&lt;String,Object&gt;接收了

方式1：可以使用List&lt;Map&lt;String,Object&gt;&gt;接收

方法2：可以添加一个@MapKey的注解

在Map&lt;String,Object&gt; selectAll上添加一个@MapKey(“id”)的注解

注意，双引号中的是查询的数据中的一个字段，之后会作为一个大map的键，而id这个键对应的值就是这个id所在的数据，即p27中查出的键值对

这波是键值对套键值对

同时，因为键值对的key是不可以重复的，所以这里要用主键或者是不会重复的字段作为参数

## p30 p31 mybatis处理模糊查询

```java
List<User> selectUserByMoHu(@Param("mohu") String mohu);
```

```java
<select id="selectUserByMoHu" resultType="com.ice.mybatis.pojo.User">
        select * from t_user where username like '%${mohu}%'
    </select>
```

1 这个时候要使用${},这样可以拼接出正确的sql（有sql注入风险）

2 或者，如果使用占位符的方式可以这样写sql（concat拼接）

```java
select * from t_user where username like concat('%',#{mohu},'%')
```

使用一个concat拼接

3 或者直接拼接（最建议的方式）

```java
select * from t_user where username like "%"#{mohu}"%"
```

注意，这里%外使用的是双引号

## p32 批量删除

sql：

```java
delete from t_user where id in (6,7)
```

mapper：

```java
void deleteMoreUser(@Param("ids") String ids);
```

xml:

```java
<delete id="deleteMoreUser">
        delete from t_user where id in (${ids})
</delete>
```

测试：

deleteMoreUser（“6,7”）

这里就必须使用${}了，因为如果使用#{}会默认多出一个单引号，这样sql就不对了

## p33 设置动态表名

有时要动态设置表名

用${}

原因同上

## p34 在新增数据时获取这个数据的自增主键

mapper：

```java
void insertByUser(User user);
```

xml:

```java
<insert id="insertByUser" useGeneratedKeys="true" keyProperty="id">
insert into t_user values(null,#{username},#{password},#{age},#{gender},#{email})
    </insert>
```

useGeneratedKeys指的是当前添加的功能的主键为自增

keyProperty指的是把自增的主键返回到对象的某个字段里，这里是id，所以测试类调用完方法后就会将id放到作为参数的User中

```java
User user = new User(null,"1","1",1,"1","1");
        userMapper.insertByUser(user);
        System.out.println(user);
```

打印出的user的id为11

## p 35 标题是搭建mybatis框架，但讲的好像是resultMap自定义映射

这个视频将的是当数据库中的字段和java中的对象属性不一致时，应该如何处理

如，在数据库中，字段名是符合mysql规范的user_name,而java中是符合java规范的userName小驼峰命名方式，这个时候查询出的数据对应不上属性名怎么办

## p36 使用全局配置处理字段名和属性名不一样的问题

方法1：

sql查询的时候起别名

```java
select user_name userName ,age from t_user
```

方法2：

mybatis核心配置文件中的setting标签中有很多封装好的映射

其中有一个叫mapUnderscoreToCamelCase 的，意思是把下划线转成小驼峰，把属性设置为true

```java
<settings>
        <setting name="mapUnderscoreToCamelCase" value="ture"/>
    </settings>
```

这样就可以继续在sql中使用select *来进行查询了

且数据库中的下划线会自动映射为小驼峰

在使用自动映射的过程中，发现自动映射失效

排查后发现是因为在实体类使用lombok（@Data），却没有对实体类进行序列化

## p37 使用resultMap处理字段名和属性名不一样的问题

书接上回

方法3：

可以在xml配置resultMap

```java
<resultMap id="userMap" type="User">
<id property="id" column="id"></id>
<result property="userName" column="user_name"></result>
<result property="password" column="password"></result>
<result property="age" column="age"></result>
<result property="sex" column="sex"></result>
</resultMap>
```

是映射主键的

是映射普通字段的

除了这两个外还有另外两个，后面几p讲

column是数据库中字段名，property是java中类的属性名

中的id是这个resultMap的id，用来给sql找到它的，type就是要映射的类

之后在之前那个sql中添加这个resultMap的映射

```java
<select id="testMohu" resultMap="userMap">
<!--select * from t_user where username like '%${mohu}%'-->
select id,user_name,password,age,sex from t_user where user_name like
concat('%',#{mohu},'%')
</select>
```

resultMap="userMap"中的userMap是刚刚说的resultMap标签中的id

## p38 处理多对一映射关系

**对一，对应的就是一个对象，对多，对应的就是一个集合**

比如员工和部门

多个员工对应一个部门，就是每一个员工都对应一个部门的对象

一个部门对应多个员工，就是每一个部门都对应一个员工的集合

## p39 使用级联处理多对一的映射关系

先添加多表联查的sql

```java
<select id="findEmp" parameterType="integer" resultMap="resultMapForFindEmp">
        select emp.*,dept.* from  emp left join  dept on emp.dept_id = dept.dept_id where emp.emp_id = #{empId}
    </select>
```

在Emp类中添加一个private Dept dept;

然后在resultMap中添加

```java
<resultMap id="resultMapForFindEmp" type="com.ice.mybatis.pojo.Emp">
        <id column="emp_id" property="empId"></id>
        <result column="emp_name" property="empName"></result>
        <result column="age" property="age"></result>
        <result column="gender" property="gender"></result>
        <result column="dept_id" property="dept.deptId"></result>
        <result column="dept_name" property="dept.deptName"></result>
    </resultMap>
```

这个配置中的dept_id对应的是sql查出的dept_id，后面的dept.deptId对应的是tpye中的实体类中创建的dept对象中的deptId属性

## p40 使用association处理多对一映射关系

```java
<resultMap id="resultMapForFindEmp" type="com.ice.mybatis.pojo.Emp">
        <id column="emp_id" property="empId"></id>
        <result column="emp_name" property="empName"></result>
        <result column="age" property="age"></result>
        <result column="gender" property="gender"></result>
        <association property="dept" javaType="com.ice.mybatis.pojo.Dept">
            <id column="dept_id" property="deptId"></id>
            <result column="dept_name" property="deptName"></result>
        </association>
    </resultMap>
```

专门用来处理多对一的映射关系（处理实体类类型的属性）

如这里的dept就是Emp中的一个属性而他本身又是一个实体类，这个时候就可以使用association

## p41 使用分步查询处理多对一的映射关系

要想清楚每一步要查什么

1 通过员工id查询员工

2 通过员工中的部门id查到部门

①查询员工信息

```java
/**
* 通过分步查询查询员工信息
* @param eid
* @return
*/
Emp getEmpByStep(@Param("empId") int emptId);
```

```java
<resultMap id="empDeptStepMap" type="Emp">
<id column="emp_id" property="empId"></id>
<result column="emp_name" property="empName"></result>
<result column="age" property="age"></result>
<result column="gender" property="gender"></result>
<!--
select：设置分步查询，查询某个属性的值的sql的标识（namespace.sqlId）
column：将sql以及查询结果中的某个字段设置为分步查询的条件
-->
<association property="dept"
select="com.atguigu.MyBatis.mapper.DeptMapper.getEmpDeptByStep" column="dept_id">
</association>
</resultMap>

<!--Emp getEmpByStep(@Param("eid") int eid);-->
<select id="getEmpByStep" resultMap="empDeptStepMap">
select * from emp where emp_id = #{empId}
</select>
```

②根据员工所对应的部门id查询部门信息

```java
/**
* 分步查询的第二步： 根据员工所对应的did查询部门信息
* @param did
* @return
*/
Dept getEmpDeptByStep(@Param("deptId") int deptId);
```

```java
<!--Dept getEmpDeptByStep(@Param("did") int did);-->
<select id="getEmpDeptByStep" resultType="Dept">
select * from dept where dept_id = #{deptId}
</select>
```

## P42 分步查询的好处：延迟加载

分步查询的优点：可以实现延迟加载
 但是必须在核心配置文件中设置全局配置信息：
 lazyLoadingEnabled：延迟加载的全局开关。当开启时，所有关联对象都会延迟加载
 aggressiveLazyLoading：当开启时，任何方法的调用都会加载该对象的所有属性。否则，每个属性会按需加载

懒加载：

比如之前的例子，查询员工的信息时，如果我调用对了查询员工信息的方法，然后获取员工的姓名而不获取员工的部门相关的属性，那么mybatis就只会调用获取员工信息的sql而不调用获取部门信息的sql

lazyLoadingEnabled开启时，就是全都延迟加载，而aggressiveLazyLoading的意思就是，当这个开启时，不管掉不掉用部门的属性，获取部门属性的那个sql都会自动加载

所以lazyLoadingEnabled开启且aggressiveLazyLoading关闭，就是实现延迟加载，即所谓的懒加载

此时就可以实现按需加载，获取的数据是什么，就只会执行相应的sql。

上面的是全局配置，如果全局配置里开了延迟加载，但是你的某一个分步查询又需要立即加载，则可通过association和collection中的fetchType属性设置当前的分步查询是否使用延迟加载， fetchType=“lazy(延迟加载)|eager(立即加载)”

## p43 一对多映射关系

直接抄笔记里的了

```java
/**
* 根据部门id查新部门以及部门中的员工信息
* @param did
* @return
*/
Dept getDeptEmpByDid(@Param("did") int did);
```

```java
<resultMap id="deptEmpMap" type="Dept">
<id property="did" column="did"></id>
<result property="dname" column="dname"></result>
<!--
ofType：设置collection标签所处理的集合属性中存储数据的类型
-->
<collection property="emps" ofType="Emp">
<id property="eid" column="eid"></id>
<result property="ename" column="ename"></result>
<result property="age" column="age"></result>
<result property="sex" column="sex"></result>
</collection>
</resultMap>
<!--Dept getDeptEmpByDid(@Param("did") int did);-->
<select id="getDeptEmpByDid" resultMap="deptEmpMap">
select dept.*,emp.* from t_dept dept left join t_emp emp on dept.did =
emp.did where dept.did = #{did}
</select>
```

## p44 分步加载实现一对多

直接抄笔记了兄弟

①查询部门信息

```java
/**
* 分步查询部门和部门中的员工
* @param did
* @return
*/
Dept getDeptByStep(@Param("did") int did);
```

```java
<resultMap id="deptEmpStep" type="Dept">
<id property="did" column="did"></id>
<result property="dname" column="dname"></result>
<collection property="emps" fetchType="eager"
select="com.atguigu.MyBatis.mapper.EmpMapper.getEmpListByDid" column="did">
</collection>
</resultMap>
<!--Dept getDeptByStep(@Param("did") int did);-->
<select id="getDeptByStep" resultMap="deptEmpStep">
select * from t_dept where did = #{did}
</select>
```

②根据部门id查询部门中的所有员工

```java
/**
* 根据部门id查询员工信息
* @param did
* @return
*/
List<Emp> getEmpListByDid(@Param("did") int did);
```

```java
<!--List<Emp> getEmpListByDid(@Param("did") int did);-->
<select id="getEmpListByDid" resultType="Emp">
select * from t_emp where did = #{did}
</select>
```

## p45 动态sql简介

多条件查询的时候有些条件没有

## p46 if标签

```java
<!--List<Emp> getEmpListByCondition(Emp emp);-->
<select id="getEmpListByMoreTJ" resultType="Emp">
select * from t_emp where 1=1
<if test="ename != '' and ename != null">
and ename = #{ename}
</if>
<if test="age != '' and age != null">
and age = #{age}
</if>
<if test="sex != '' and sex != null">
and sex = #{sex}
</if>
</select>
```

## p47 where标签

where和if一般结合使用：
 a&gt;若where标签中的if条件都不满足，则where标签没有任何功能，即不会添加where关键字
 b&gt;若where标签中的if条件满足，则where标签会自动添加where关键字，并将条件最前方多余的
 and去掉
 注意：where标签不能去掉条件最后多余的and

```java
<select id="getEmpListByMoreTJ2" resultType="Emp">
select * from t_emp
<where>
<if test="ename != '' and ename != null">
ename = #{ename}
</if>
<if test="age != '' and age != null">
and age = #{age}
</if>
<if test="sex != '' and sex != null">
and sex = #{sex}
</if>
</where>
</select>
```

**不使用where标签的话，也可以在where后面加一个1=1**

## p48 trim标签

感觉没有where好用

trim用于去掉或添加标签中的内容
 常用属性：
 prefix：在trim标签中的内容的前面添加某些内容
 prefixOverrides：在trim标签中的内容的前面去掉某些内容
 suffix：在trim标签中的内容的后面添加某些内容
 suffixOverrides：在trim标签中的内容的后面去掉某些内容

```java
<select id="getEmpListByMoreTJ" resultType="Emp">
select * from t_emp
<trim prefix="where" suffixOverrides="and">
<if test="ename != '' and ename != null">
    ename = #{ename} and
</if>
<if test="age != '' and age != null">
age = #{age} and
</if>
<if test="sex != '' and sex != null">
sex = #{sex}
</if>
</trim>
</select>
```

## p49 choose when otherwise 标签

choose、when、 otherwise相当于if…else if…else

```java
<!--List<Emp> getEmpListByChoose(Emp emp);-->
<select id="getEmpListByChoose" resultType="Emp">
select <include refid="empColumns"></include> from t_emp
<where>
<choose>
<when test="ename != '' and ename != null">
ename = #{ename}
</when>
<when test="age != '' and age != null">
age = #{age}
</when>
<when test="sex != '' and sex != null">
sex = #{sex}
</when>
<when test="email != '' and email != null">
email = #{email}
</when>
</choose>
</where>
</select>
```

## p50 51 foreach 批量添加和批量删除

```java
<!--int insertMoreEmp(@Pamram("emps")List<Emp> emps);-->
<insert id="insertMoreEmp">
insert into t_emp values
<foreach collection="emps" item="emp" separator=",">
(null,#{emp.ename},#{emp.age},#{emp.sex},#{emp.email},null)
</foreach>
</insert>
<!--int deleteMoreByArray(int[] eids);-->
<delete id="deleteMoreByArray">
delete from t_emp where
<foreach collection="eids" item="eid" separator="or">
eid = #{eid}
</foreach>
</delete>
<!--int deleteMoreByArray(int[] eids);-->
<delete id="deleteMoreByArray">
delete from t_emp where eid in
<foreach collection="eids" item="eid" separator="," open="(" close=")">
    #{eid}
</foreach>
</delete>
```

## p52 sql标签

sql片段，可以记录一段公共sql片段，在使用的地方通过include标签进行引入

```java
<sql id="empColumns">
eid,ename,age,sex,did
</sql>
select <include refid="empColumns"></include> from t_emp
```

## p53 Mybatis 的一级缓存

一级缓存是**SqlSession**级别的，通过同一个SqlSession查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问

比如在测试类中，调用了

User user = userMapper.getUserById(“1”);

之后再User user2 = userMapper.getUserById(“1”);

你会发现只运行了一次sql，这是因为缓存把第一次运行的结果保存下来了

## p54 一级缓存失效的四种情况

1. 不同的SqlSession对应不同的一级缓存

两个不同的SqlSession不用同一个缓存

1. 同一个SqlSession但是查询条件不同

查询条件不同，是不同的sql了，肯定也不一样

1. 同一个SqlSession两次查询期间执行了任何一次增删改操作

执行增删改操作之后，就不会从缓存中获取数据，而是重新从数据库获取数据，因为增删改会修改数据库数据，那缓存中的数据可就不一定对了

1. 同一个SqlSession两次查询期间手动清空了缓存

这个就不用说了，清空了，肯定重新查

sqlSession.clearCache() 这是用来清除一级缓存的

## p55 mybatis的二级缓存

二级缓存是SqlSessionFactory级别，通过**同一个SqlSessionFactory创建的SqlSession**查询的结果会被缓存；此后若再次执行相同的查询语句，结果就会从缓存中获取
 二级缓存开启的条件：
 a&gt;在核心配置文件中，设置全局配置属性cacheEnabled=“true”，默认为true，不需要设置
 b&gt;在映射文件中设置标签 
 c&gt;二级缓存必须在SqlSession关闭或提交之后有效

sqlSession.close()

d&gt;查询的数据所转换的实体类类型必须实现序列化的接口
 使二级缓存失效的情况：
 两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效

## p56 二级缓存相关配置

在mapper配置文件中添加的cache标签可以设置一些属性：

①eviction属性：缓存回收策略，默认的是 LRU。

LRU（Least Recently Used） – 最近最少使用的：移除最长时间不被使用的对象。

FIFO（First in First out） – 先进先出：按对象进入缓存的顺序来移除它们。

SOFT – 软引用：移除基于垃圾回收器状态和软引用规则的对象。

WEAK – 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象。

②flushInterval属性：刷新间隔，单位毫秒

默认情况是不设置，也就是没有刷新间隔，缓存仅仅调用语句时刷新

③size属性：引用数目，正整数

代表缓存最多可以存储多少个对象，太大容易导致内存溢出
 ④readOnly属性：只读， true/false

true：只读缓存；会给所有调用者返回缓存对象的相同实例。因此这些对象不能被修改。这提供了 很重要的性能优势。

false：读写缓存；会返回缓存对象的拷贝（通过序列化）。这会慢一些，但是安全，因此默认是false。

**查询缓存顺序**

先查询二级缓存，因为二级缓存中可能会有其他程序已经查出来的数据，可以拿来直接使用。

如果二级缓存没有命中，再查询一级缓存

如果一级缓存也没有命中，则查询数据库

SqlSession关闭之后，一级缓存中的数据会写入二级缓存

## p57整合第三方缓存

是针对二级缓存的

了解，知道mybatis可以整合第三方缓存就可以了，所以还是直接复制哈

### 1 添加依赖

```java
<!-- Mybatis EHCache整合包 -->
<dependency>
<groupId>org.mybatis.caches</groupId>
<artifactId>mybatis-ehcache</artifactId>
<version>1.2.1</version>
</dependency>
<!-- slf4j日志门面的一个具体实现 -->
<dependency>
<groupId>ch.qos.logback</groupId>
<artifactId>logback-classic</artifactId>
<version>1.2.3</version>
</dependency>
```

### 2 各jar包作用


### 3 创建EHCache的配置文件ehcache.xml

```java
<?xml version="1.0" encoding="utf-8" ?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
<!-- 磁盘保存路径 -->
<diskStore path="D:\atguigu\ehcache"/>
<defaultCache
maxElementsInMemory="1000"
maxElementsOnDisk="10000000"
eternal="false"
overflowToDisk="true"
timeToIdleSeconds="120"
timeToLiveSeconds="120"
diskExpiryThreadIntervalSeconds="120"
memoryStoreEvictionPolicy="LRU">
</defaultCache>
</ehcache>
```

### 4 设置二级缓存的类型

这个是写在映射文件里的

```java
<cache type="org.mybatis.caches.ehcache.EhcacheCache"/>
```

### 5 加入logback日志

存在SLF4J时，作为简易日志的log4j将失效，此时我们需要借助SLF4J的具体实现logback来打印日
 志。 创建logback的配置文件logback.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="true">
<!-- 指定日志输出的位置 -->
<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
<encoder>
<!-- 日志输出的格式 -->
<!-- 按照顺序分别是： 时间、日志级别、线程名称、打印日志的类、日志主体内容、换行
-->
<pattern>[%d{HH:mm:ss.SSS}] [%-5level] [%thread] [%logger]
[%msg]%n</pattern>
</encoder>
</appender>
<!-- 设置全局日志级别。日志级别按顺序分别是： DEBUG、INFO、WARN、ERROR -->
<!-- 指定任何一个日志级别都只打印当前级别和后面级别的日志。 -->
<root level="DEBUG">
<!-- 指定打印日志的appender，这里通过“STDOUT”引用了前面配置的appender -->
<appender-ref ref="STDOUT" />
</root>
<!-- 根据特殊需求指定局部日志级别 -->
<logger name="com.atguigu.crowd.mapper" level="DEBUG"/>
</configuration>
```

### 6 EHCache配置文件说明


