---
layout:  post
title:   java重新开始2 尚硅谷最新SSM教程逐P笔记 2_spring部分
date:   2023-05-31 15:38:38
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-spring
-java
-mybatis

---


网址：【【尚硅谷】SSM框架全套教程，MyBatis+Spring+SpringMVC+SSM整合一套通关】https://www.bilibili.com/video/BV1Ya411S7aT?p=4&amp;vd_source=10e3dfac95ac3a6883b1f8a6c3bc65d5

 [最近看视频学习的感悟](http://t.csdn.cn/gZTsL) [JAVA重新开始](http://t.csdn.cn/x2EqR)

这个笔记是我根据视频的P数来记的，把一些网上随时可以搜到的（比如mybatis历史之类的）部分删减，记录下了自己觉得较为重要的知识点,同时还记录了老师在课上讲的，但是可能并没有在官方给的笔记里展现出来的东西。

目前更新到p93

## p63 spring概述

Spring：让java更简单

Spring 框架来创建性能好、易于测试、可重用的代码。

创建性能好：

以前我们在控制层 下面是service层，下面是Dao层

每一层都要new一个对象 ，现在我们可以直接接收Spring直接提供给我们的对象

易于测试：

可以使用单元测试来对我们的代码进行测试

可重用：

之前：

事务管理：不好封装

## p64 framework简介和特性

1 特性

- 非侵入式：使用 Spring Framework 开发应用程序时，Spring 对应用程序本身的结构影响非常

小。对领域模型可以做到零污染；对功能性组件也只需要使用几个简单的注解进行标记，完全不会

破坏原有结构，反而能将组件结构进一步简化。这就使得基于 Spring Framework 开发应用程序

时结构清晰、简洁优雅。

- 控制反转：IOC——Inversion of Control，翻转资源获取方向。把自己创建资源、向环境索取资源

变成环境将资源准备好，我们享受资源注入。

- 面向切面编程：AOP——Aspect Oriented Programming，在不修改源代码的基础上增强代码功

能。

- 容器：Spring IOC 是一个容器，因为它包含并且管理组件对象的生命周期。组件享受到了容器化

的管理，替程序员屏蔽了组件创建过程中的大量细节，极大的降低了使用门槛，大幅度提高了开发

效率。

- 组件化：Spring 实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用 XML

和 Java 注解组合这些对象。这使得我们可以基于一个个功能明确、边界清晰的组件有条不紊的搭

建超大型复杂应用系统。

- 
 声明式：很多以前需要编写代码才能实现的功能，现在只需要声明需求即可由框架代为实现。
- 
 一站式：在 IOC 和 AOP 的基础上可以整合各种企业应用的开源框架和优秀的第三方类库。而且

Spring 旗下的项目已经覆盖了广泛领域，很多方面的功能性需求可以在 Spring Framework 的基

础上全部使用 Spring 来实现。

2、Spring Framework五大 功能模块


## p65 ioc思想和DI

IOC：Inversion of Control，翻译过来是**反转控制**。

**理解：**

原来是我们自己获取容器资源，这就要求我们对我们需要获取的资源了如指掌

现在反过来，资源自己给我们提供资源，我们不需要了解我们获取的资源，这波就是**反转**

##### ①获取资源的传统方式

自己做饭：买菜、洗菜、择菜、改刀、炒菜，全过程参与，费时费力，必须清楚了解资源创建整个过程中的全部细节且熟练掌握。

在应用程序中的组件需要获取资源时，传统的方式是组件**主动**的从容器中获取所需要的资源，在这样的模式下开发人员往往需要知道在具体容器中特定资源的获取方式，增加了学习成本，同时降低了开发效率。

##### ②反转控制方式获取资源

点外卖：下单、等、吃，省时省力，不必关心资源创建过程的所有细节。

反转控制的思想完全颠覆了应用程序组件获取资源的传统方式：反转了资源的获取方向——改由容器主动的将资源推送给需要的组件，开发人员不需要知道容器是如何创建资源对象的，只需要提供接收资源的方式即可，极大的降低了学习成本，提高了开发的效率。这种行为也称为查找的**被动**形式。

**很多时候，点外卖要比自己做的还要香，比如我们想要单例模式，以前要自己写，现在可以直接让Spring给我一个**

##### ③DI

DI：Dependency Injection，翻译过来是**依赖注入**。

DI 是 IOC 的另一种表述方式：即组件以一些预先定义好的方式（例如：setter 方法）接受来自于容器的资源注入。相对于IOC而言，这种表述更直接。

所以结论是：IOC 就是一种反转控制的思想， 而 DI 是对 IOC 的一种具体实现。

## p66 ioc容器在Spring中的实现

Spring 的 IOC 容器就是 IOC 思想的一个落地的产品实现。IOC 容器中管理的组件也叫做 bean。在创建bean 之前，首先需要创建 IOC 容器。Spring 提供了 IOC 容器的两种实现方式：

##### ①BeanFactory

这是 IOC 容器的基本实现，是 Spring 内部使用的接口。面向 Spring 本身，**不提供给开发人员使用**。

##### ②ApplicationContext

BeanFactory 的子接口，提供了更多高级特性。面向Spring 的使用者，几乎所有场合都使用ApplicationContext 而不是底层的 BeanFactory。

##### ③ApplicationContext的主要实现类


## p67 Spring的入门案例

##### ①创建Maven Module

##### ②引入依赖

```java
<dependencies>
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

##### ③创建类HelloWorld

```java
public class HelloWorld {
    public void sayHello(){
        System.out.println("helloworld");
    }
}
```

##### ⑤在Spring的配置文件中配置bean

新建spring的配置文件，最好命名为applicationContext


![img](https://img-blog.csdnimg.cn/img_convert/456034ef2d7935cf2a7bac2382f1ffdf.png)


![img](https://img-blog.csdnimg.cn/img_convert/88e042b456d04319db03783f9966812e.png)

```java
<!--
	配置HelloWorld所对应的bean，即将HelloWorld的对象交给Spring的IOC容器管理
	通过bean标签配置IOC容器所管理的bean
	属性：
		id：设置bean的唯一标识
		class：设置bean所对应类型的全类名
-->
<bean id="helloworld" class="com.atguigu.spring.bean.HelloWorld"></bean>
```

##### ⑥创建测试类测试

```java
@Test
public void testHelloWorld(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
    HelloWorld helloworld = (HelloWorld) ac.getBean("helloworld");
    helloworld.sayHello();
}
```

##### ⑦注意

Spring 底层默认通过反射技术调用组件类的无参构造器来创建组件对象，这一点需要注意。如果在需要无参构造器时，没有无参构造器，则会抛出下面的异常：

>org.springframework.beans.factory.BeanCreationException: Error creating bean with name

## P68 iOC容器创建对象的方式

一个普通的User类

```java
<bean id="User" class="com.ice.spring.pojo.User"></bean>
```

然后在测试类中：

```java
@Test
    public void test(){
        ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
        User user=ac.getBean(User.class);
        System.out.println(user);
    }
```

## P69 获取bean的三种方式和注意事项

我们最常用的是根据类型获取

##### ①方式一：根据id获取

由于 id 属性指定了 bean 的唯一标识，所以根据 bean 标签的 id 属性可以精确获取到一个组件对象。

上个实验中我们使用的就是这种方式。

##### ②方式二：根据类型获取

```java
@Test
public void testHelloWorld(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
    HelloWorld bean = ac.getBean(HelloWorld.class);
    bean.sayHello();
}
```

##### ③方式三：根据id和类型

```java
@Test
public void testHelloWorld(){
    ApplicationContext ac = newClassPathXmlApplicationContext("applicationContext.xml");
    HelloWorld bean = ac.getBean("helloworld", HelloWorld.class);
    bean.sayHello();
}
```

##### ④注意

当根据类型获取bean时，要求IOC容器中指定类型的bean有且只能有一个

当IOC容器中一共配置了两个：

```java
<bean id="helloworldOne" class="com.atguigu.spring.bean.HelloWorld"></bean>
<bean id="helloworldTwo" class="com.atguigu.spring.bean.HelloWorld"></bean>
```

根据类型获取时会抛出异常：

>org.springframework.beans.factory.NoUniqueBeanDefinitionException: No qualifying bean

##### ⑤扩展

如果组件类实现了接口，根据接口类型可以获取 bean 吗？

>可以，前提是bean唯一

如果一个接口有多个实现类，这些实现类都配置了 bean，根据接口类型可以获取 bean 吗？

>不行，因为bean不唯一

##### ⑥结论

根据类型来获取bean时，在满足bean唯一性的前提下，其实只是看：『对象 **instanceof** 指定的类

型』的返回结果，只要返回的是true就可以认定为和类型匹配，能够获取到。

## P70 依赖注入之setter注入

在之前例子的基础上，在配置文件中配置bean的时候使用property标签配置属性值

```java
<bean id="User" class="com.ice.spring.pojo.User">
        <property name="age" value="12"></property>
        <property name="email">
            <value><![CDATA[2427328505@qq.com]]></value>
        </property>
    </bean>
```

## P71 依赖注入之构造器注入

构造器注入用的不多

##### ①在Student类中添加有参构造

```java
public Student(Integer id, String name, Integer age, String sex) {
    this.id = id;
    this.name = name;
    this.age = age;
    this.sex = sex;
}
```

##### ②配置bean

```java
<bean id="studentTwo" class="com.atguigu.spring.bean.Student">
    <constructor-arg value="1002"></constructor-arg>
    <constructor-arg value="李四"></constructor-arg>
    <constructor-arg value="33"></constructor-arg>
    <constructor-arg value="女"></constructor-arg>
</bean>
```

>注意：

##### ③测试

```java
@Test
public void testDIBySet(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("springdi.xml");
    Student studentOne = ac.getBean("studentTwo", Student.class);
    System.out.println(studentOne);
}
```

## P72 依赖注入之特殊值处理

##### 1 null

```java
<property name="name">
	<null />
</property>
```

>注意：

##### 2 特殊字符

当需要使用&lt; &gt;等字符时，需要避免这两个符号和xml标签中的&lt;&gt;的冲突

方法1：

```java
<!-- 小于号在XML文档中用来定义标签的开始，不能随便使用 -->
<!-- 解决方案一：使用XML实体来代替 -->
<property name="expression" value="a &lt; b"/>
```

方法2：

CDATA节

```java
<property name="expression">
    <!-- 解决方案二：使用CDATA节 -->
    <!-- CDATA中的C代表Character，是文本、字符的含义，CDATA就表示纯文本数据 -->
    <!-- XML解析器看到CDATA节就知道这里是纯文本，就不会当作XML标签或属性来解析 -->
    <!-- 所以CDATA节中写什么符号都随意 -->
    <value><![CDATA[a < b]]></value>
</property>
```

## p73 为类类型属性赋值(引用外部bean)

##### ①创建班级类Clazz

```java
@Data
public class Clazz implements Serializable {
    private Integer clazzId;
    private String clazzName;
}
```

##### ②修改Student类

在Student类中添加以下代码：

```java
private Clazz clazz;
public Clazz getClazz() {
    return clazz;
}
public void setClazz(Clazz clazz) {
    this.clazz = clazz;
}
```

##### ③方式一：引用外部已声明的bean

配置Clazz类型的bean：

```java
<bean id="clazzOne" class="com.atguigu.spring.bean.Clazz">
    <property name="clazzId" value="1111"></property>
    <property name="clazzName" value="财源滚滚班"></property>
</bean>
```

为Student中的clazz属性赋值：

```java
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
</bean>
```

错误演示：

```java
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <property name="clazz" value="clazzOne"></property>
</bean>
```

>如果错把ref属性写成了value属性，会抛出异常： Caused by: java.lang.IllegalStateException:

## p74 为类类型属性赋值（内部bean和级联的方式）

##### ④方式二：内部bean

```java
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <property name="clazz">
        <!-- 在一个bean中再声明一个bean就是内部bean -->
        <!-- 内部bean只能用于给属性赋值，不能在外部通过IOC容器获取，因此可以省略id属性 -->
        <bean id="clazzInner" class="com.atguigu.spring.bean.Clazz">
            <property name="clazzId" value="2222"></property>
            <property name="clazzName" value="远大前程班"></property>
        </bean>
    </property>
</bean>
```

##### ③方式三：级联属性赋值

```java
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- 一定先引用某个bean为属性赋值，才可以使用级联方式更新属性 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="clazz.clazzId" value="3333"></property>
    <property name="clazz.clazzName" value="最强王者班"></property>
</bean>
```

## p75 为数组类型赋值

##### ①修改Student类

在Student类中添加以下代码：

```java
private String[] hobbies;
public String[] getHobbies() {
    return hobbies;
}
public void setHobbies(String[] hobbies) {
    this.hobbies = hobbies;
}
```

##### ②配置bean

```java
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="hobbies">
        <array>
            <value>抽烟</value>
            <value>喝酒</value>
            <value>烫头</value>
        </array>
    </property>
</bean>
```

## p76 为list集合类型赋值

##### ①为List集合类型属性赋值

在Clazz类中添加以下代码：

```java
private List<Student> students;
public List<Student> getStudents() {
    return students;
}
public void setStudents(List<Student> students) {
    this.students = students;
}
```

配置bean：

```java
<bean id="clazzTwo" class="com.atguigu.spring.bean.Clazz">
    <property name="clazzId" value="4444"></property>
    <property name="clazzName" value="Javaee0222"></property>
    <property name="students">
        <list>
            <ref bean="studentOne"></ref>
            <ref bean="studentTwo"></ref>
            <ref bean="studentThree"></ref>
        </list>
    </property>
</bean>
```

>若为Set集合类型属性赋值，只需要将其中的list标签改为set标签即可

## p77 为map集合类型赋值

##### ②为Map集合类型属性赋值

创建教师类Teacher：

```java
@Data
public class Teacher implements Serializable {
    private Integer teacherId;
    private String teacherName;
}
```

在Student类中添加以下代码：

```java
private Map<String, Teacher> teacherMap;
```

配置bean：

```java
<bean id="teacherOne" class="com.atguigu.spring.bean.Teacher">
    <property name="teacherId" value="10010"></property>
    <property name="teacherName" value="大宝"></property>
</bean>
<bean id="teacherTwo" class="com.atguigu.spring.bean.Teacher">
    <property name="teacherId" value="10086"></property>
    <property name="teacherName" value="二宝"></property>
</bean>
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <property name="id" value="1004"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="teacherMap">
        <map>
            <entry>
                <key>
                    <value>10010</value>
                </key>
                <ref bean="teacherOne"></ref>
            </entry>
            <entry>
                <key>
                    <value>10086</value>
                </key>
                <ref bean="teacherTwo"></ref>
            </entry>
        </map>
    </property>
</bean>
```

##### ③引用集合类型的bean

```java
<!--list集合类型的bean-->
<util:list id="students">
    <ref bean="studentOne"></ref>
    <ref bean="studentTwo"></ref>
    <ref bean="studentThree"></ref>
</util:list>
<!--map集合类型的bean-->
<util:map id="teacherMap">
    <entry>
        <key>
            <value>10010</value>
        </key>
        <ref bean="teacherOne"></ref>
    </entry>
    <entry>
        <key>
            <value>10086</value>
        </key>
        <ref bean="teacherTwo"></ref>
    </entry>
</util:map>
<bean id="clazzTwo" class="com.atguigu.spring.bean.Clazz">
    <property name="students" ref="students"></property>
</bean>
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="hobbies">
        <array>
            <value>抽烟</value>
            <value>喝酒</value>
            <value>烫头</value>
        </array>
    </property>
    <property name="teacherMap" ref="teacherMap"></property>
</bean>
```

>使用util:list、util:map标签必须引入相应的命名空间，可以通过idea的提示功能选择

## p78 依赖注入之p命名空间

这个基本上不用，简单了解

引入p命名空间后，可以通过以下方式为bean的各个属性赋值

```java
<bean id="studentSix" class="com.atguigu.spring.bean.Student"
      p:id="1006" p:name="小明" p:clazz-ref="clazzOne" p:teacherMap-ref="teacherMap"></bean>
```

## p79 spring管理数据源和引入外部文件

##### ①加入依赖

```java
<!-- MySQL驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.16</version>
</dependency>
<!-- 数据源 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.0.31</version>
</dependency>
```

##### ②创建外部属性文件

jdbc.properties

```java
jdbc.user=root
jdbc.password=atguigu
jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
jdbc.driver=com.mysql.cj.jdbc.Driver
```

##### ③引入属性文件

```java
<!-- 引入外部属性文件 -->
<context:property-placeholder location="classpath:jdbc.properties"/>
```

##### ④配置bean

```java
<bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="url" value="${jdbc.url}"/>
    <property name="driverClassName" value="${jdbc.driver}"/>
    <property name="username" value="${jdbc.user}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>
```

##### ⑤测试

```java
@Test
public void testDataSource() throws SQLException {
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-datasource.xml");
    DataSource dataSource = ac.getBean(DataSource.class);
    Connection connection = dataSource.getConnection();
    System.out.println(connection);
}
```

## p80 bean的作用域

##### ①概念

在Spring中可以通过配置bean标签的scope属性来指定bean的作用域范围，各取值含义参加下表：


如果是在WebApplicationContext环境下还会有另外两个作用域（但不常用）：


##### ②创建类User

```java
@Data
public class User implements Serializable {
private Integer id;
private String username;
private String password;
private Integer age;
}
```

##### ③配置bean

```java
<!-- scope属性：取值singleton（默认值），bean在IOC容器中只有一个实例，IOC容器初始化时创建
对象 -->
<!-- scope属性：取值prototype，bean在IOC容器中可以有多个实例，getBean()时创建对象 -->
<bean class="com.atguigu.bean.User" scope="prototype"></bean>
```

##### ④测试

```java
@Test
public void testBeanScope(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-scope.xml");
    User user1 = ac.getBean(User.class);
    User user2 = ac.getBean(User.class);
    System.out.println(user1==user2);
}
```

## p81-82 bean的生命周期

生命周期了解即可，这里复制笔记

##### ①具体的生命周期过程

- bean对象创建（调用无参构造器）
- 给bean对象设置属性
- bean对象初始化之前操作（由bean的后置处理器负责）
- bean对象初始化（需在配置bean时指定初始化方法）
- bean对象初始化之后操作（由bean的后置处理器负责）
- bean对象就绪可以使用
- bean对象销毁（需在配置bean时指定销毁方法）
- IOC容器关闭

##### ②修改类User

```java
public class User {
    private Integer id;
    private String username;
    private String password;
    private Integer age;
    public User() {
        System.out.println("生命周期：1、创建对象");
    }
    public User(Integer id, String username, String password, Integer age) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.age = age;
    }
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        System.out.println("生命周期：2、依赖注入");
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
    public void initMethod(){
        System.out.println("生命周期：3、初始化");
    }
    public void destroyMethod(){
        System.out.println("生命周期：5、销毁");
    }
    @Override
    public String toString() {
        return "User{" +
            "id=" + id +
            ", username='" + username + '\'' +
            ", password='" + password + '\'' +
            ", age=" + age +
            '}';
    }
}
```

>注意其中的initMethod()和destroyMethod()，可以通过配置bean指定为初始化和销毁的方法

##### ③配置bean

```java
<!-- 使用init-method属性指定初始化方法 -->
<!-- 使用destroy-method属性指定销毁方法 -->
<bean class="com.atguigu.bean.User" scope="prototype" init-method="initMethod"destroy-method="destroyMethod">
    <property name="id" value="1001"></property>
    <property name="username" value="admin"></property>
    <property name="password" value="123456"></property>
    <property name="age" value="23"></property>
</bean>
```

##### ④测试

```java
@Test
public void testLife(){
    ClassPathXmlApplicationContext ac = newClassPathXmlApplicationContext("spring-lifecycle.xml");
    User bean = ac.getBean(User.class);
    System.out.println("生命周期：4、通过IOC容器获取bean并使用");
    ac.close();
}
```

##### ⑤bean的后置处理器

bean的后置处理器会在生命周期的初始化前后添加额外的操作，需要实现BeanPostProcessor接口，

且配置到IOC容器中，需要注意的是，bean后置处理器不是单独针对某一个bean生效，而是针对IOC容器中所有bean都会执行

创建bean的后置处理器：

```java
package com.atguigu.spring.process;
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;
public class MyBeanProcessor implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName)
        throws BeansException {
        System.out.println("☆☆☆" + beanName + " = " + bean);
        return bean;
    }
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName)
        throws BeansException {
        System.out.println("★★★" + beanName + " = " + bean);
        return bean;
    }
}
```

在IOC容器中配置后置处理器：

>&lt;bean id="myBeanProcessor"class=“com.atguigu.spring.process.MyBeanProcessor”/&gt;

## p83 FactoryBean

##### ①简介

FactoryBean是Spring提供的一种整合第三方框架的常用机制。和普通的bean不同，配置一个FactoryBean类型的bean，在获取bean的时候得到的并不是class属性中配置的这个类的对象，而是getObject()方法的返回值。通过这种机制，Spring可以帮我们把复杂组件创建的详细过程和繁琐细节都屏蔽起来，只把最简洁的使用界面展示给我们。

将来我们整合Mybatis时，Spring就是通过FactoryBean机制来帮我们创建SqlSessionFactory对象的。

##### ②创建类UserFactoryBean

```java
public class UserFactoryBean implements FactoryBean<User> {
    @Override
    public User getObject() throws Exception {
        return new User();
    }
    @Override
    public Class<?> getObjectType() {
        return User.class;
    }
}
```

##### ③配置bean

```java
<bean id="user" class="com.atguigu.bean.UserFactoryBean"></bean>
```

##### ④测试

```java
@Test
public void testUserFactoryBean(){
    //获取IOC容器
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-factorybean.xml");
    User user = (User) ac.getBean("user");
    System.out.println(user);
}
```

## p84-86 基于xml的自动装配

自动装配的意思是：

本来一个UserCoontroller中有个对象是UserService

本来配置bean的时候需要用来配置这个对象，现在添加一个byName或者byType就可以自动装配了

bytype:controller中有一个UserService，然后配置文件（配置bean的xml）中有一个类型是UserService，就会自动配置这个

>自动装配：

##### ①场景模拟

创建类UserController

```java
public class UserController {
    private UserService userService;
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
    public void saveUser(){
        userService.saveUser();
    }
}
```

创建接口UserService

```java
public interface UserService {
	void saveUser();
}
```

创建类UserServiceImpl实现接口UserService

```java
public class UserServiceImpl implements UserService {
    private UserDao userDao;
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    @Override
    public void saveUser() {
        userDao.saveUser();
    }
}
```

创建接口UserDao

```java
public interface UserDao {
	void saveUser();
}
```

创建类UserDaoImpl实现接口UserDao

```java
public class UserDaoImpl implements UserDao {
    @Override
    public void saveUser() {
        System.out.println("保存成功");
    }
}
```

##### ②配置bean

>使用bean标签的autowire属性设置自动装配效果

```java
<bean id="userController"class="com.atguigu.autowire.xml.controller.UserController" autowire="byType">
</bean>
<bean id="userService"class="com.atguigu.autowire.xml.service.impl.UserServiceImpl" autowire="byType">
</bean>
<bean id="userDao" class="com.atguigu.autowire.xml.dao.impl.UserDaoImpl"></bean>
```

>自动装配方式：byName

```java
<bean id="userController"class="com.atguigu.autowire.xml.controller.UserController" autowire="byName">
</bean>
<bean id="userService"class="com.atguigu.autowire.xml.service.impl.UserServiceImpl" autowire="byName">
</bean>
<bean id="userServiceImpl"class="com.atguigu.autowire.xml.service.impl.UserServiceImpl" autowire="byName">
</bean>
<bean id="userDao" class="com.atguigu.autowire.xml.dao.impl.UserDaoImpl">
</bean>
<bean id="userDaoImpl" class="com.atguigu.autowire.xml.dao.impl.UserDaoImpl">
</bean>
```

##### ③测试

```java
@Test
public void testAutoWireByXML(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("autowire-xml.xml");
    UserController userController = ac.getBean(UserController.class);
    userController.saveUser();
}
```

## p87-89 基于注解管理的注解和扫描

介绍：在类上添加一个注解，然后在spring的配置文件中扫描到这个类，然后spring就会自动执行操作（不需要自己写bean了）

##### ③新建Maven Module

```java
<dependencies>
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <!-- junit测试 -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

##### ④创建Spring配置文件

##### ⑤标识组件的常用注解

>@Component：将类标识为普通组件

问：以上四个注解有什么关系和区别？

@Controller、@Service、@Repository这三个注解只是在@Component注解的基础上起了三个新的名字。

对于Spring使用IOC容器管理这些组件来说没有区别。所以@Controller、@Service、@Repository这三个注解只是给开发人员看的，让我们能够便于分辨组件的作用。

注意：虽然它们本质上一样，但是为了代码的可读性，为了程序结构严谨我们肯定不能随便胡乱标记。

##### ⑥创建组件

创建控制层组件

```java
@Controller
public class UserController {
}
```

创建接口UserService

```java
public interface UserService {
}
```

创建业务层组件UserServiceImpl

```java
@Service
public class UserServiceImpl implements UserService {
}
```

创建接口UserDao

```java
public interface UserDao {
}
```

创建持久层组件UserDaoImpl

```java
@Repository
public class UserDaoImpl implements UserDao {
}
```

##### ⑦扫描组件

情况一：最基本的扫描方式

记录4: beans的命名空间中，在使用扫描包时，要引入的命名空间为

 xmlns:context=“http://www.springframework.org/schema/context”

和

 http://www.springframework.org/schema/context
 ​ http://www.springframework.org/schema/context/spring-context-4.2.xsd
 ​

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context-4.2.xsd
         ">
   <context:component-scan base-package="com.ice">
   </context:component-scan>
</beans>
<context:component-scan base-package="com.atguigu">
</context:component-scan>
```

情况二：指定要排除的组件

```java
<context:component-scan base-package="com.atguigu">
    <!-- context:exclude-filter标签：指定排除规则 -->
    <!--
        type：设置排除或包含的依据
        type="annotation"，根据注解排除，expression中设置要排除的注解的全类名
        type="assignable"，根据类型排除，expression中设置要排除的类型的全类名
    -->
    <context:exclude-filter type="annotation"expression="org.springframework.stereotype.Controller"/>
    <!--<context:exclude-filter type="assignable"expression="com.atguigu.controller.UserController"/>-->
</context:component-scan>
```

情况三：仅扫描指定组件

```java
<context:component-scan base-package="com.atguigu" use-default-filters="false">
    <!-- context:include-filter标签：指定在原有扫描规则的基础上追加的规则 -->
    <!-- use-default-filters属性：取值false表示关闭默认扫描规则 -->
    <!-- 此时必须设置use-default-filters="false"，因为默认规则即扫描指定包下所有类 -->
    <!--
        type：设置排除或包含的依据
        type="annotation"，根据注解排除，expression中设置要排除的注解的全类名
        type="assignable"，根据类型排除，expression中设置要排除的类型的全类名
     -->
    <context:include-filter type="annotation"expression="org.springframework.stereotype.Controller"/>
    <!--<context:include-filter type="assignable"expression="com.atguigu.controller.UserController"/>-->
</context:component-scan>
```

##### ⑧测试

```java
@Test
public void testAutowireByAnnotation(){
    ApplicationContext ac = new
        ClassPathXmlApplicationContext("applicationContext.xml");
    UserController userController = ac.getBean(UserController.class);
    System.out.println(userController);
    UserService userService = ac.getBean(UserService.class);
    System.out.println(userService);
    UserDao userDao = ac.getBean(UserDao.class);
    System.out.println(userDao);
}
```

## p90 基于注解管理bean之bean的id

##### ⑨组件所对应的bean的id

在我们使用XML方式管理bean的时候，每个bean都有一个唯一标识，便于在其他地方引用。现在使用

注解后，每个组件仍然应该有一个唯一标识。

>默认情况

## p91-93 基于注解的自动装配

@Autowired自动装配的作用

原来Controller中调用Service：

```java
public class UserController {
    private UserService userService;
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
    public void saveUser(){
        userService.saveUser();
    }
}
```

现在：

```java
public class UserController {
    @Autowired
    private UserService userService; 
}
```

##### ①场景模拟

>参考基于xml的自动装配

##### ②@Autowired注解

在成员变量上直接标记@Autowired注解即可完成自动装配，不需要提供setXxx()方法。以后我们在项目中的正式用法就是这样。

```java
@Controller
public class UserController {
    @Autowired
    private UserService userService;
    public void saveUser(){
        userService.saveUser();
    }
}
```

```java
public interface UserService {
    void saveUser();
}
@Service
public class UserServiceImpl implements UserService {
    @Autowired
    private UserDao userDao;
    @Override
    public void saveUser() {
        userDao.saveUser();
    }
}
```

```java
public interface UserDao {
	void saveUser();
}
```

```java
@Repository
public class UserDaoImpl implements UserDao {
    @Override
    public void saveUser() {
        System.out.println("保存成功");
    }
}
```

##### ③@Autowired注解其他细节

>@Autowired注解可以标记在构造器和set方法上

```java
@Controller
public class UserController {
    private UserService userService;
    @Autowired
    public UserController(UserService userService){
        this.userService = userService;
    }
    public void saveUser(){
        userService.saveUser();
    }
}
```

```java
@Controller
public class UserController {
    private UserService userService;
    @Autowired
    public void setUserService(UserService userService){
        this.userService = userService;
    }
    public void saveUser(){
        userService.saveUser();
    }
}
```

##### ④@Autowired工作流程

- 首先根据所需要的组件类型到IOC容器中查找 
 <ul>
  - 能够找到唯一的bean：直接执行装配
  - 如果完全找不到匹配这个类型的bean：装配失败
  - 和所需类型匹配的bean不止一个 
   <ul>
    - 没有@Qualifier注解：根据@Autowired标记位置成员变量的变量名作为bean的id进行匹配
    - 能够找到：执行装配
    - 找不到：装配失败
    - 使用@Qualifier注解：根据@Qualifier注解中指定的名称作为bean的id进行匹配
    - 能够找到：执行装配
    - 找不到：装配失败
   </ul>
 </ul>

```java
@Controller
public class UserController {
    @Autowired
    @Qualifier("userServiceImpl")
    private UserService userService;
    public void saveUser(){
        userService.saveUser();
    }
}
```

>@Autowired中有属性required，默认值为true，因此在自动装配无法找到相应的bean时，会装配失败

