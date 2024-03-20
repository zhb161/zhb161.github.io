---
layout:  post
title:   尚硅谷vue笔记 详细讲解版（尚硅谷 天禹老师）
date:   2023-05-31 15:37:15
author:  'ice'
header-img: 'img/post-bg-2015.jpg'
catalog:   false
tags:
-vue.js
-javascript
-前端

---


视频：【尚硅谷Vue2.0+Vue3.0全套教程丨vuejs从入门到精通】https://www.bilibili.com/video/BV1Zy4y1K7SH?vd_source=10e3dfac95ac3a6883b1f8a6c3bc65d5

>看了很多市面上以后的笔记，大多都是复制粘贴代码，让我看的知其然而不知其所以然，于是打算自己写一下这个课程的笔记，把一些老师的讲解结合自己的理解也写下来

教程内容：

1.vue基础
 2.vue-cli
 3.vue-router
 4.vuex
 5.element-ui
 6.vue3

注：因为笔者学习过程中需要参与一个小项目，该项目需要使用到vue，但是记详细的讲解比较较为耗时，所以在1.10之后的笔记是只记录使用方法和案例，不添加详细讲解。实际上，您可以直接访问官网的文档教程，如果您看了我的笔记的1.10之前的内容，理解官网的教程应该就比较简单了，如果有不理解的，再去看老师的讲解视频，个人觉得这是较快的学习方法（当然 ，时间充裕的，最好去听老师讲的课）

## 第1章 vue核心

### 1.1 vue简介

#### 1.1.1vue是什么

一套用于构建用户界面的渐进式js框架

- 
 构建用户界面：我只关注，你把数据给我，我怎么把数据变成界面
- 
 渐进式：可以自底向上逐层应用：
 <ul>
  - 简单应用：只需要一个小巧的核心库
  - 复杂应用：可以引入各式各样的vue插件
 </ul>

#### 1.1.2 谁开发的


![img](https://img-blog.csdnimg.cn/img_convert/6ffa67589a68032c270d63f22ca461e3.png)


![img](https://img-blog.csdnimg.cn/img_convert/f6378ccf6a3e525860e3126b512eec9d.png)

#### 1.1.3 vue的特点

1. 采用组件化模式，提高代码复用率、且让代码更好维护。

组件化：


![img](https://img-blog.csdnimg.cn/img_convert/706266efb6145fd4b38a793da20f070e.png)

以后其他人想用这个activity功能，直接应用我的这个文件就行

更好维护：哪个部分出了问题，就到哪个组件维护

1. 声明式编码，让编码人员无需直接操作DOM,提高开发效率。

js：用代码拼接html 这是命令式编码


![img](https://img-blog.csdnimg.cn/img_convert/1a847ad915313efa100a405e72202883.png)

命令式：同学，我渴了，你往前走两步，到饮水机面前，拿出杯子，倒点水，回头走到我旁边，往我嘴里倒水

声明式：同学，我渴了。然后同学就把水装给我了

1. 使用虚拟DOM+优秀的Dif算法，尽量复用DOM节点。

咱们还是用js举例

原来你声明了变量，赋值以后写到html页面上，之后，如果你的数据变了，刷新页面的时候，相当于把原来的删除了，又从头添加了数据。


![img](https://img-blog.csdnimg.cn/img_convert/fc3bcf9c93f4d5b86afcdb6d39017ec1.png)

而vue呢，先把三个数据转换成虚拟dom，然后再转换成页面中的真实dom

数据变化之后，又生成了新的虚拟dom，他会把新的虚拟dom和原来的dom进行比较，然后会把原本的数据复用，再添加上多出来的dom（这里的赵六）


![img](https://img-blog.csdnimg.cn/img_convert/224600aeba3fef4ca0ce714e84ce9c1e.png)

1. 学习Vue之前要掌握的javaScript基础知识：
    ES6语法规范 结构函数，模板字符串，箭头函数
    ES6模块化 默认暴露，同意暴露，分别暴露
    包管理器 npm yarn cnpm
    原型、原型链
    数组常用方法 过滤一个数组，
    axios
    promise

当然，如果哪个不会，老师也会简单回顾一下

#### 1.1.4 vue网站简单了解（vue2文档）

 [Vue.js (vuejs.org)](https://v2.cn.vuejs.org/)

1. 教程

按照教程说的一步一步来

1. API

不会的就找字典

1. 风格指南

会教你怎么写出优雅的vue代码

1. 示例

看示例的时候，往右划一划，就能看到代码

1. cookbook

编码技巧： 1 js基本功 2 vue代码一些小技巧

指南和cookbook的不同：指南教你什么好，什么不好；cookbook教你实用的技巧

1. 工具 核心插件

公司开发时用到的 ，很重要

1. Awssome vue/浏览和vue相关的包

很多vue的周边库（steam的创意工坊）

#### 1.1.5 搭建vue开发环境

根据文档，安装


![img](https://img-blog.csdnimg.cn/img_convert/6326b5cecd4c31a87e507cefcb4ca6ca.png)

我们可以看到，一个是直接scipt引入vue，另外一个是使用npm安装

咱们先直接用引用

开发时，最好使用开发版本

点击后，自动下载，上面的是开发版，下面的是生产版，过会会进行对比


![img](https://img-blog.csdnimg.cn/img_convert/e81eb19d7e71811a6e62b123382eca37.png)

ok，我们在桌面新建一个文件夹，叫vue_basic

用vs code打开（不会有人前端已经学到vue了还不知道什么是vscode吧，不会吧不会吧）

把两个文件放在js文件夹中，新建html文件，新建完，！＋回车；html结构就出来了

**文件夹结构：**


![img](https://img-blog.csdnimg.cn/img_convert/20f8b91831c1400743a5846ecc82f66e.png)

**引入vue**

```java
<script type="text/javascript" src="../js/vue.js"></script>
```


![img](https://img-blog.csdnimg.cn/img_convert/700fe6ac51c40767251a5e91d4d74d82.png)

如何证明我们引入了vue呢？

右键，在浏览器中打开（记得CTRL+s保存）

f12查看控制台，可以看到两个提示，一个说建议用开发工具开发vue，另一个说引入的vue有点大，不建议在生产环境中使用

输入vue，敲回车，发现有了构造方法，说明引用成功了


![img](https://img-blog.csdnimg.cn/img_convert/d89d7918a8a29b0081804ea06baf88af.png)

说回刚刚的问题，如何下载浏览器vue的开发工具，edge下载扩展


![img](https://img-blog.csdnimg.cn/img_convert/a89c14e0d1b89a361145d7ac944ca636.png)

还要点上允许文件访问


![img](https://img-blog.csdnimg.cn/img_convert/22d85031fe7355c4d579da082ea63a84.png)

另外一个提示我们如何隐藏呢，这是vue的全局配置中的一个属性，我们可以在文件中修改默认值


![img](https://img-blog.csdnimg.cn/img_convert/8f8379d4ba3587968cdb4bb879522837.png)


![img](https://img-blog.csdnimg.cn/img_convert/6167d1e067b1cb1dc926951025246b25.png)

### 1.2 初识vue

#### 1.2.1 vue小案例

首先，我们要添加一个存放页面的容器

容器，一般在11行，是一切的开始

输入 div#root 回车 得到：


![img](https://img-blog.csdnimg.cn/img_convert/17b7c83a6c3b20bc222fc5e8c9df8cb4.png)

创建一个Vue对象 在19行


![img](https://img-blog.csdnimg.cn/img_convert/f840a69e62fc1c73c55279fd513047d1.png)

然后我们需要

##### 配置对象

>什么叫配置对象：对象中有需要配置的属性：如anxios中要配置url，这个url你不能写成ura，因为不存在这个属性，url对应的值写在’'中，这是有规范的


![img](https://img-blog.csdnimg.cn/img_convert/97cb6e00cf754db52f7567b3b6f0ae09.png)

好，我们开始写vue的配置对象


el是element的简称，里面的#root类似于css中的id选择器，没有第二十行的这个配置的时候，vue对象和id为root的容器是互相看不到的，加上之后，他们就互相匹配了

>el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。


![img](https://img-blog.csdnimg.cn/img_convert/a3ce09ea15a9004ddfb1b4dee906fdaf.png)


我们之前在容器中写的是hhh，那我们想在我们的实例中动态的存放那个位置填写的文字，怎么办呢

很自然的，第二个属性：data

>data中用于存储数据，数据供el所指定的容器去使用,值我们暂时先写成一个对象(以后可能写成一个函数)

这里用到了双大括号（插值语法，后面会讲到），这个实际上就是分隔符区分data的数据


![img](https://img-blog.csdnimg.cn/img_convert/4852cba99f2e3295dae33e6c6d402d30.png)


![img](https://img-blog.csdnimg.cn/img_convert/b2f29c54b76481c6a35e4b1221b63fbf.png)

写到这我们发现，const x一点用也没有，我们可以去掉，完全不受影响


![img](https://img-blog.csdnimg.cn/img_convert/702f208523e89709e9c1099c6a8a965d.png)

##### 总结

1. 
 想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象：
2. 
 root容器里的代码依然符html规范只不过混入了一些特殊的vue语法：
3. 
 root容器里的代码被称为【Vue模板】

#### 1.2.2 分析小案例

1. 容器和实例之间的关系是一对一的，一一对应
2. 以后如果数据多了，会有组件功能来分担数据
3. =={<!-- -->{}}==中必须写成js表达式

区分js表达式和js代码

- js表达式：可以生成一个值，可以放在任何一个需要值的地方 
 <ul>
  - a
  - a+b
  - Data.now() 生成当前时间戳
  - demo(1) 函数调用表达式
  - x==y ? ‘a’:‘b’ 三元表达式
  - 以上的东西都是可以在左边用一个const x= 接住的
 </ul>
- js代码（语句） 
 <ul>
  - if(){}
  - for(){}
 </ul>

1. vue开发者工具


![img](https://img-blog.csdnimg.cn/img_convert/d0ab333a05b1f7c31fd0814c5377947e.png)

可以直接在这里修改数据

1. 一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新

### 1.3 模板语法

#### 1.3.1 效果

实际上，模板语法有两大类，一类就是{<!-- -->{}}，插值语法

还有一类叫指令语法

比如，我们想在一个<a href=""></a>标签里，动态存入href的值，该怎么做呢，第一反应肯定是加一个{<!-- -->{}}，我们试试看：


![img](https://img-blog.csdnimg.cn/img_convert/3ba4c05c333ebabb8457ca2dbbd3b621.png)

我们发现，并没有帮我转换，看一下控制台的报错：


![img](https://img-blog.csdnimg.cn/img_convert/c0a261fb52e24b50867df79659ef6859.png)

说以前这样子写是可以的，但是现在不行了，建议我们用v-bind或者：来写

#### 1.3.2 指令语法

引入 v-bind：

我们在href前添加v-bind:

```java
<a v-bind:href="url">点我跳转</a>
```

发现url动态的显示在href中了：


![img](https://img-blog.csdnimg.cn/img_convert/74268564bce98ebb1d87d91eb3bffa5e.png)

><code>v-bind:</code>后的属性值后的双引号中的也是js表达式,且可以简写为 <code>：</code>

简写：

```java
<a :href="url">点我跳转</a>
```

>插值模板主要用在标签体中

总结：

Vue模板语法有2大类：
 1.插值语法：
 功能：用于解析标签体内容。
 写法：{<!-- -->{xxx}}:xx是的s表达式。且可以直接读取到data中的所有属性。
 2.指令语法：
 功能：用于解析标签（包括：标签属性、标签体内容、绑定事件…）。
 举例：v-bind:href="xxx"域筒写为：:href="xxx",xxx同样要列js表达式，且以直接读取到data中的所有属性.
 备注：Vue中有根多的指令，且形式都是：v-???,此处我们只是拿v-bind举个例子。

如果一个页面有多个地方，需要name这个变量怎么办：

我们可以name1，name2但是可读性不高，所以我们可以在data中再新建对象，如图：


![img](https://img-blog.csdnimg.cn/img_convert/53f05c3411dafca26b6fdad005377129.png)

使用这样的方法区分不同的变量

### 1.4 数据绑定

#### 1.4.1 单向数据绑定

v-bind是单向数据绑定

<input v-bind:value="name">

在这个input框中填写数据，data中name的值不会变，因为数据只能从data中到v-bind中

实例1：

容器：

```java
<div id="root">
      <input v-bind:value="name" />
      <hr/>
      {{name}}
    </div>
```

一开始：


![img](https://img-blog.csdnimg.cn/img_convert/5409733eb469421b4752b887bbe1bdd3.png)

input中输入数据后：


![img](https://img-blog.csdnimg.cn/img_convert/d92660a4834c7132d31b82e98117bb26.png)

#### 1.4.2 双向数据绑定

引出新的指令模板 v-model

```java
<input v-model:value="name" />
```

v-model可以双向绑定，即在value中的数据也可以同步到data中：


![img](https://img-blog.csdnimg.cn/img_convert/79585676cc85ceb9b5c07fc3a6390c05.png)

总结：

v-model只能用在表单类元素中（输入类元素）

也就是说，有一个属性是value的元素

v-model:value=可以简写成v-model=

### 番外 el和data的两种写法

正常说讲到组件才要讲这个，但是组件内容太多了，所以拆到这里说一下

#### el

之前我们是在data中，通过el属性来绑定vue实例和容器的。

除此之外，我们可以通过挂载的方式绑定

```java
<script>     
//创建Vue实例
      const v = new Vue({
        data: {
          name: "五六七",
        },
      });
      v.$mount("#root");
    </script>
```

v.$mount的这个操作叫挂载

这两种方式都可以，第二种比较灵活一点

#### data

原来的方法：

```java
data:{
name:''
}
<script>
 const v = new Vue({
        data:{
			name:''
			}
      });
      v.$mount("#root");
</script>
```

这是对象式写法，还有一种写法，叫函数式

函数式：

```java
<script>
 const v = new Vue({
        data: function(){
            return{
                name:'尚硅谷'
            }
        }
      });
      v.$mount("#root");
</script>
```

el 两种方法都可以

但是data，**以后用到组件的时候，只可以用函数式**，不然会报错，我们到时候会讲到

由vue管理的函数，不可以用箭头函数（es6中的东西），写了箭头函数后，this就不再是vue实例了

### 1.5 MVVM模型

Vue的设计受到了MVVM模型的启发，设计时参考了这个模型

1. M 模型（model） 对应data中的数据
2. V 视图（View） 模板（页面结构）
3. VM 视图模型（ViewModel） Vue实例对象


![img](https://img-blog.csdnimg.cn/img_convert/4fb8a61c053f169d3d9dc292302f03f1.png)

其实主流的前端框架都是这样

所以我们经常使用vm这个变量名表示Vue实例

**观察发现：**
 1.data中所有的属性，最后都出现在了vm身上.
 2.vm身上所有的属性及Vue原型上所有属性，在Vue模版中都可以直接使用.

console.log一下vue实例


![img](https://img-blog.csdnimg.cn/img_convert/95024a9805846a24d4c38e58ca804034.png)

下面这些v的属性数据都可以写在模板中


![img](https://img-blog.csdnimg.cn/img_convert/a9c222ac0fd6a0f4b24c1e65671bfd1f.png)

原型中的也可以写在里面（当然，写也没什么意义，这些是用来调用的方法）


![img](https://img-blog.csdnimg.cn/img_convert/8e099711dd7727edaa5d2c06193aa376.png)

### 1.6 数据代理

#### 1.6.1 回顾 Object.defineProperty方法

用于给对象添加属性

需要三个参数

第一个是对象 第二个是属性名 第三个是配置项

```java
<script type="text/javascript">

        let person={
            age:'18',
            name:'桃桃'
        }
        Object.defineProperty(person,'sex',{
            value:'女'
        })
        console.log(person)
    </script>
```


![img](https://img-blog.csdnimg.cn/img_convert/dd2a7b36d2364acfa34058f96154891b.png)

用这种方法添加的属性，在遍历时不会参与遍历


![img](https://img-blog.csdnimg.cn/img_convert/b9c1c7386aab47fb0613664f4a4c092b.png)

如果想要这个属性也可以参与遍历，在用方法添加时，在配置项中添加一个叫**enumerable**的属性

```java
<script>
Object.defineProperty(person,'sex',{
            value:'女',
            enumerable:true
        })
    </script>
```

用这种方法添加的属性，值也是不可以修改的：


![img](https://img-blog.csdnimg.cn/img_convert/a316074dd9bfad18fdab0508acf1d580.png)

要是想修改，添加属性**writable**

同理，也无法删除，想要删除，添加属性**configurable**

这些是基本的配置项，除此之外，我们可以添加一些高级的配置项 get set

比如我们不想要age的值是固定的，我们想要age的值是取决于一个叫做number的变量，然后number的值变了，age的值就会变，我们怎么写呢


![img](https://img-blog.csdnimg.cn/img_convert/e0818c9e32a87a86dfa362cf186093be.png)

我们现在想要number值变了，我们的值也变，怎么办呢，使用Object.defineProperty方法配置项中的get属性

```java
<script type="text/javascript">
      let number = "女";
      let person = {
        age: "18",
        name: "桃桃",
      };
      Object.defineProperty(person, "sex", {
        // enumerable:true,
        // writable:true,
        // configurable:true
        get:function(){
            return number
        }
      });
      console.log(person);
    </script>
```


![img](https://img-blog.csdnimg.cn/img_convert/19f87c0aa29c90c6bab047fa54f56b3e.png)

每一次访问sex，都会触发get方法的调用

set方法：

```java
<script type="text/javascript">
      let number = "女";
      let person = {
        age: "18",
        name: "桃桃",
      };
      Object.defineProperty(person, "sex", {
        // enumerable:true,
        // writable:true,
        // configurable:true
        get:function(){
            return number
        },
        set:function(value){
            number=value
        }
      });
      console.log(person);
    </script>
```

每次有人修改sex的值，都会调用set方法

#### 1.6.2 何为数据代理

通过一个对象代理对另一个对象中属性的操作

比如有一个obj1对象，其中一个属性是x，我们想通过另一个obj2对象来获取和修改obj1中x属性的值，应该怎么做呢，这就可以用到上面学的东西

```java
<script type="text/javascript">
       let obj1={x:100}
       let obj2={y:200}
       Object.defineProperty(obj2,'x',{
        get(){
            return obj1.x;
        },
        set(value){
            obj1.x=value;
        }
       })
      </script>
```


![img](https://img-blog.csdnimg.cn/img_convert/c4405de5434750c9476f19db154c83e0.png)

>模板语法中数据的值（data属性中数据的值）就是通过数据代理存放到vm（vue实例）中的

#### 1.6.3 数据代理在vue中的使用

1.Vue中的数据代理：
 通过VM对象代理data对像中属性的操作（读/写）
 2.Vue中数据代理的好处：
 更加方便的操作data中的数据
 3.基本原理：
 通过Object,defineProperty()把data对象中所有属性添加到外vm上，
 为每一个添加到vm上的属性，都指定一个getter/setter.
 在getter/setter内部去操作（读/写）data中对应的属性.


![img](https://img-blog.csdnimg.cn/img_convert/269a41d94026401154fa2c7ef4622dd4.png)

options是Vue的配置对象的意思

vm._data实际上就是我们传给它的data

所以以下这两种表达方式都是可 以的


![img](https://img-blog.csdnimg.cn/img_convert/fbbb9b7c13d0bd8dd327d76f3e1de1e8.png)

vm.data是用的数据代理

数据代理图示：


![img](https://img-blog.csdnimg.cn/img_convert/1c8e5f21a4f2e46ae2f54195bcf0aa6d.png)

### 1.7 事件处理

#### 1.7.1 事件的基本使用：

1. 使用v-on:xxx或@xxx绑定事件，其中xxx是事件名：
2. 事件的回调需要配置在methods对象中，最终会在vm上：
3. methods中配置的函数，不要用箭头函数！否则this就不是vm了：
4. methods中配置的函数，都是被Vue所管理的函数，this的指向是vm或组件实例对象：
5. @click="demo”和@click="demo($event)"效果一到，但后者可以传参


![img](https://img-blog.csdnimg.cn/img_convert/fba9f249fe24e98a469b6660e127918d.png)

在button中，绑定一个v-on指令，在vue实例中添加一个新属性，methods，在里面添加方法，：

```java
<body>
    <div id="root">
        <h1>{{name}}
        </h1>

        <button v-on:click="clickme">别点我</button>
    </div>


</body>
<script type="text/javascript">

    new Vue(
        {
            el: '#root',
            data: {
                name: '桃桃'
            },
            methods:{
                clickme(){
                    alert('让你别点，你个小坏蛋')
                }
            }
        }
    )

</script>
```

此时在页面中点击按钮，就会弹出弹框

如果我们在方法中添加一个参数，

```java
click(a){
console.log(a);
}
```

在页面中点击时，发现打印在控制台的是点击事件


![img](https://img-blog.csdnimg.cn/img_convert/edd7678b052bbab151ffae20d317865e.png)

这是老师以前讲的事件event（建议这部分去视频里听一下，因为我以前没学过，肯定讲不明白这个是什么东西，这个在视频的p14 事件处理中）

我们把参数改为event，打印event.target这个是打印出事件触发的元素，也就是我们的button标签


![img](https://img-blog.csdnimg.cn/img_convert/7e3086c5751ad75ea067cf1a2f3123a3.png)


![img](https://img-blog.csdnimg.cn/img_convert/17ed57423d65da7a162710510ff43a3d.png)

注意，所有被vue管理的函数不可以用箭头函数

>简写 v-on简写成@ v-on:click @click

如果想要传参的话，就在click后双引号里方法名后加括号，里面写参数，不传参可以 不加括号

```java
<button v-on:click="clickme('hello')">别点我</button>
```


![img](https://img-blog.csdnimg.cn/img_convert/dd354e86acfb398579268dce16ca7830.png)

当然，也可以直接传已定义的变量

```java
<button v-on:click="clickme(name)">别点我</button>
```


![img](https://img-blog.csdnimg.cn/img_convert/f3c7459dadcd94f79c88e0ff57a02ba3.png)

这样的话，就把之前的event搞丢了，可以在括号中添加$event来接受事件

#### 1.7.2 事件修饰符

Vue中的事件修饰符：

1. prevent:阻止默认事件（常用）

```java
<a href="www.baidu.com" @click="sum">点我</a>
```

正常点击这个按钮的时候，会先触发sum方法，然后跳转页面，如果我们不想a标签触发其默认事件（访问链接），我们可以在click后添加prevent,就不会访问了

```java
<a href="www.baidu.com" @click.prevent="sum">点我</a>
```

2.stop:阻止事件冒泡（常用）：

当存在标签嵌套，且内外的标签都有调用的事件时，点击里面的标签，会像冒泡一样，触发外面标签的事件：

```java
<div @click="sum2">
<button  @click="sum">点我</button>
</div>
```

如以上的代码，点击按钮时，会先触发sum方法，然后冒泡触发sum2方法，如果外面像阻止冒泡，可以在里面的click后添加.stop以阻止事件冒泡

3.once:事件只触发一次（常用）：

这个就很好理解了，事件只触发一次

后面三个不常用，我没怎么听懂，有学习需要的建议原视频

4.capture:使用事件的捕获模式：
 5.self:只有event.target是当前操作的元素时才触发事件：
 6.passive:事件的默认行为立即执行，无需等待事件回调执行完毕：

如果需要多个修饰符，比如既要阻止冒泡，又要阻止默认行为，可以@click.prevent.stop这代表先阻止默认行为，再阻止冒泡。实际上他们哪个先阻止，效果是一样的

#### 1.7.3 键盘事件

keydown，按下去就触发事件

keyup，按下去，抬上来之后才出发事件

event:当前事件

event.target：当前事件操作的元素

event.target.value 这是这个例子中input的value

```java
<input @keyup='print'>

print(event){
console.log(event.target.value);
}
```

效果：


![img](https://img-blog.csdnimg.cn/img_convert/1ac05d361db65d828e8bd0eea6d43424.png)

那问题来了，如果我们不想每次按键的时候都在控制台输出，而是按特定的案件才会输出，怎么办呢

我们知道每一个按键都有一个keyCode值（没事，我也是才知道），我们可以先在控制台输出一下


![img](https://img-blog.csdnimg.cn/img_convert/fd53da13ea089ad4f401dc8a7345cc65.png)

可以看到，每次按完按键都会输出按键对应的键码，


![img](https://img-blog.csdnimg.cn/img_convert/2e8d70763955c9c57ddc2074eebdef85.png)

我们输入回车，发现对应的键码是13，所以我们可以在方法中添加一个校验，如果触发当前事件的按键键码不是13，就不执行，这样，就只有回车时才会打印了。


![img](https://img-blog.csdnimg.cn/img_convert/21ecd26588bd0887d63c4067eced7532.png)

实际上，以上操作可以直接在@keyup后加.enter来完成：

```java
<input @keyup.enter='print'>
print(event){
console.log(event.target.value);
}
```

这里的enter是回车键的别名，@keyup.enter='print’的意思是按下enter键后会触发print方法

键盘的每一个按键，除了键码外也有自己对应的名字，keyu后可以添加每一个按键的名字

我们可以这样获取当前按键的名字和键码：

```java
print(event) {
   console.log(event.key,event.keyCode);
       }
```

.key就是按键的名字


![img](https://img-blog.csdnimg.cn/img_convert/aa1c7db6c9e641ac6026c4a264107a5f.png)

如果要按下ctrl键触发，可以写@keyup.Control或者@keyup.17

如果要求按下ctrl+y触发，我们可以写@keyup.ctrl.y

这里的ctrl是别名

注意项：

1. 
 <p>Vue中常用的按键别名：<br>
   回车=&gt;enter<br>
   删除=&gt;delete(捕获“删除”和“退格”键)<br>
   退出=&gt;esc<br>
   空格=&gt;space<br>
   换行=&gt;tab<br>
   上=&gt;up<br>
   下=&gt;down<br>
   左=&gt;1eft<br>
   右=&gt;right</p>
2. 
 Vue未提供别名的按键，可以使用按键原始的key值去绑定，但由两个单词组成的要注意要转为kebab-case(短横线命名)
3. 
 <p>系统修饰键（用法特殊）：ctrl、alt、shift、meta(win)<br>
   (I).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。<br>
   (2).配合keydown使用：正常触发事件。</p>
4. 
 也可以使用keyCode去指定具体的按键（不推荐）
5. 
 Vue.config.keyCodes.自定义键名=键码，可以去定制按键别名


![img](https://img-blog.csdnimg.cn/img_convert/91f83970a59e341f88c82853550d96a5.png)

### 1.8 计算属性

我们现在要完成一个需求，就是在两个input框中分别填写姓和名，要求自动在后面拼写出完整的姓名

为了横向对比，我们分别用{<!-- -->{}}，methods，和计算属性完成这个需求

#### 1.8.1 {{}}

这个就太简单了

直接上代码

```java
<body>
    <div id="root">
姓：<input v-model="firstName"><br/>
名：<input v-model="lastName"><br/>
全名：<span>{{firstName}}+{{lastName}}</span>
    </div>
</body>
<script type="text/javascript">

    new Vue(
        {
            el: '#root',
            data: {
                firstName: '',
                lastName:''
            }
        }
    )

</script>
```

#### 1.8.2 methods

可以在插值语法中调用方法，然后在方法中返回

注意，如果在{<!-- -->{}}中的方法不加（），在页面中显示的是方法体，加了（）之后，返回的才是方法中return的值，这和之前的绑定事件不一样

```java
<body>
    <div id="root">
姓：<input v-model="firstName"><br/>
名：<input v-model="lastName"><br/>
全名：<span>{{fullname()}}</span>

    </div>


</body>
<script type="text/javascript">

    new Vue(
        {
            el: '#root',
            data: {
                firstName: '',
                lastName:''
            },
            methods: {
                fullname(){
                    return this.firstName+this.lastName
                }
            }
        }
    )

</script>
```

#### 1.8.3 computed 计算属性

计算属性：
 1,定义：要用的属性不存在，要通过己有属性计算得来。
 2,原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
 3.get函数什么时候执行？
 (1).初次读取时会执行一次。
 (2).当依赖的数据发生改变时会被再次调用。
 4.优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
 5.备注：
 1,计算属性最终会出现在vm上，直接读取使用即可。
 2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

当我们需要的数据是从两个已有的属性中计算得来的，这个计算得来的新属性就被称作计算属性

```java
<script type="text/javascript">
    new Vue(
        {
            el: '#root',
            data: {
                firstName: '',
                lastName: ''
            },
            computed: {
                fullname: {
                    get() {
                        return this.firstName + '-' + this.lastName
                    }
                }
            }
        }
    )

</script>
```

computed中的都是计算属性，和data很像，但是有get和set方法，底层是Objcet.defineproperty实现的，然后插值模板中直接写属性名就可以 了： {<!-- -->{fullname}}

#### 1.8.4 计算属性的简写

当某一个计算属性只有get，没有set的时候，可以简写成函数的样子

```java
<script type="text/javascript">
    new Vue(
        {
            el: '#root',
            data: {
                firstName: '',
                lastName: ''
            },
            computed: {
                fullname: function(){       //这一行也可以写成  fullname(){             
                        return this.firstName + '-' + this.lastName            
                }
            }
        }
    )

</script>
```

当然不要看到他长得像函数，就把他当成函数了，在{<!-- -->{}}中使用的时候，还是不能添加括号的。

### 1.9 监视属性

**推荐插件**

Vue 3 Snippets 会提示vue代码

#### 1.9.1 watch 监视属性

就是添加了一个新的配置项，watch，

当watch中监视的数据发生改变时，就会调用watch中的方法

直接引出watch中的方法，handler：

```java
<body>
    <div id="root">
        姓：<input v-model="firstName"><br />
        <button @click="firstName++">点我</button>
    </div>


</body>
<script type="text/javascript">

    new Vue(
        {
            el: '#root',
            data: {
                firstName: 1
            },
            watch: {
                firstName: {
                    handler() {
                        console.log("firstname被改了")
                    }

                }
            }
        }
    )

</script>
```

在页面中点击按钮修改firstName的值的时候，就会调用watch中的handler方法

handler可以接收两个参数，第一个是修改后的数据，第二个是修改前的数据：

```java
handler(newvalue,oldvalue) {
         console.log("firstname被改了" +newvalue+"   "+oldvalue)
   }
```


![img](https://img-blog.csdnimg.cn/img_convert/363067d8263559daf4150a402f9534bd.png)

watch是在数据被修改之后，才会触发，如果在配置项中添加一个immediate属性，就会在一开始加载页面的时候，就触发一次：

```java
watch: {
	firstName: {
             handler() {
immediate:true，
console.log("firstname被改了")
                    }

                }
```

同时，计算属性中的数据也可以在watch中被监视，使用方法相同 。

除了直接在vue()中配置以外，watch还可以在vue实例中手动配置：

```java
<script type="text/javascript">

    var vm = new Vue(
        {
            el: '#root',
            data: {
                firstName: 1
            }
        }
    )
    vm.$watch('firstName', {
        handler(newvalue, oldvalue) {
            console.log("firstname被改了" + newvalue + "     " + oldvalue)
        }
    })

</script>
```

记得在vm.$watch()中，firstName要添加单引号，这是因为js中对象（还是变量？我不太清楚）需要用单引号表示，我们在vue中没有添加单引号是因为我们简写了。

#### 1.9.3 深度监视

事情是这样的，当我们date中存储一个对象number，里面有数据a和b，我们改变这个a的值时，想要监视a的变化，而不是监视整个number的变化，该怎么做呢

```java
<div id="root">
{{number.a}}
<button  @click="number.a++">点我增加</button>
    </div>
    <script type="text/javascript">
        new Vue({
            el:'#root',
            data:{
               number:{
                a:1,
                b:1
               }
            
            },
            watch:{
                'number.a':{
                    handler(a,b){
                        console.log("我又被改了"+a+b);
                    }
                }
            }
        }       
        )
    </script>
```

没错，方法就是直接使用number.a，但是注意，我们在number.a边上添加了单引号，这是为什么呢。
 实际上，我们在使用这些变量名时都是引用的key，在语法规范中，key就是要添加单引号，但当只有一个单词时，在vue框架中可以省略这个单引号，但是当不是一个单词时，就要把单引号重新加上

那如果我们想要当number中的a或者b任意一个改变了，就检测到number，我们该怎么做呢

```java
watch:{
                'number':{
                    handler(a,b){
                        console.log("我又被改了"+a+b);
                    }
                }
            }
```

我们发现，直接使用number，不起作用。

实际上，number是这个对象的key，number后面的大括号实际上是这个对象的地址值，我们这样写，监视的就是对象的地址值，a变了，b变了，但是地址值是不会变的。

如何让watch监视number中的值呢，我们在watch的number中添加一个配置项deep：

```java
watch:{
                number:{
                    deep:true,
                    handler(a,b){
                        console.log("我又被改了"+a+b);
                    }
                }
            }
```

这样就会监视number中的数据的改变

#### 1.9.4 监视的简写

当你的监视项只有一个handler时，就可以简写，就好像计算属性，当只有get方法的时候，就可以简写

```java
//原来的
watch:{
                number:{
                    handler(a,b){
                        console.log("我又被改了"+a+b);
                    }
                }
            }
//修改后的：
 watch:{
                number(a,b){
                    
                        console.log("我又被改了"+a+b);
                    }
            }
```

或者，使用$f符添加，和之前的一样

```java
vm.$watch('number',{
            deep:true,
            handler(a,b){
                console.log("我被修改啦"+a+b)
            }
        })
```

或者简写模式：

```java
vm.$watch('number',function(a,b){
                console.log("我被修改啦"+a+b)
            }
        )
```

#### 1.9.5 computed和watch的区别

总结：
 computed和watch之间的区别：
 1 computed能完成的功能，watch都可以完成。
 2 watch能完成的功能，computed.不一定能完成，例如：watch可以进行异步操作。

两个重要的小原则：

1. 所有被Vue管理的函数，最好写成普通函数，这样this的指向才是vm或组件实例对象。
2. 所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等），最好写成箭头函数，这样this的指向才是vm或组件实例对象。

### 1.8 class和style样式

#### 1.8.1 class样式

我们使用:class来绑定动态的样式

```java
<div id="root">
        <!-- 字符串写法，适用于：样式的类名不确定，需要动态指定 -->
        <div class="basic" :class="mood">{{number.a}}</div>
        <!-- 数组写法，适用于：要绑定的样式个数不确定，名字也不能确定 -->
        <div class="basic" :class="moodArr">{{number.b}}</div>
        <!-- 对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
        <div class="basic" :class="moodObj">{{number.b}}</div>

    </div>
...
data:{
               number:{
                a:1,
                b:2,
                
               },
               mood:'happy',
               moodArr:['happy'],
               moodObj:{
                happy:true
               }
            },
```

肯定的不需要改变的样式就放在class中，需要变化的就放在:class中

#### 1.8.2 style样式

正常的内联style样式：

```java
<div class="basic" style="background-color:red">测试</div>
···

使用动态的style样式
​```html
        <div class="basic" :style="styleObj">{{number.b}}</div>
...
data:{
               styleObj:{
                backgroundColor:'red'
               }
            },
```

在style前面添加一个:就可以了，和class一样

总结：
 绑定样式：
 1 c1ass样式
 写法：c1ass=“xxx”xxx可以是字符串、对象、数组。
 字符串写法适用于：类名不确定，要动态获取。
 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定。
 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。
 2 style样式
 :style=”{fontsize:Xxx)“其中xxx是动态值。
 :style=”[a,b]"其中a、b是样式对象。

### 1.9 条件渲染

**v-show**

```java
<h1 v-show="true"></h1>
```

当v-show后面的双引号中可以是true，false，1===3（false），或者是一个data中的变量a：

```java
<h1 v-show="a"></h1>
...
data:{
a:true
}
```

**v-if**

```java
<h1 v-if="true"></h1>
```

v-show是节点还在，只是动态的控制他的隐藏或者显示，而v-if是把整个节点全都弄没了

**v-else-if****v-else**

```java
<h1 v-if="n===1">1</h1>
        <h1 v-else-if="n===2">2</h1>
        <h1 v-else-if="n===3">3</h1>
        <h1 v-else>4</h1>
```

这四个需要连在一起，不可以被打断

后面的用的比较多
 当我有三个相同判断条件的想简写：

```java
<h1 v-if="n===1">1</h1>
        <h1 v-if="n===1">2</h1>
        <h1 v-if="n===1">3</h1>
```

如上，三个的判断条件都是一样的，该如何简化呢，第一反应肯定是在外面包上一个div：

```java
<div v-if="n===1">
		<h1>1</h1>
        <h1>2</h1>
        <h1>3</h1>
</div>
```

但是这样会破坏我们页面的结构，比如我们要找body下的h1，就找不到了，所以我们可以使用另外一个标签：template

```java
<template v-if="n===1">
		<h1>1</h1>
        <h1>2</h1>
        <h1>3</h1>
</template>
```

这个标签不会破坏页面的结构，但是template只能和v-if配合使用，不能和v-show配合使用

### 1.10 列表渲染

#### 1.10.1 基本列表


**v-for** 类似于for循环，
 当我们想要实现类似于下图的效果时，肯定是不能写死数据的，这就要我们通过遍历的方式显示数据![img](https://img-blog.csdnimg.cn/c65cde1b0acc4bc69f0defd7340acf6e.png)

```java
<!-- 遍历数组 -->
      在遍历数组时，数组元素后面的一个参数，是遍历时的key值，因为我们这里没有自定义key，所以默认是012
      <ul>
        <li v-for="(person,b) in persons">
          {{b}}--{{person.name}}--{{person.age}}
        </li>
      </ul>
      <!-- 遍历对象 -->
      遍历对象时，括号中第一个参数是对象中键值对的值，第二个参数是键值对的键，第三个参数是这个这条遍历的数据的key
      <ul>
        <li v-for="(value,key,b) in car">{{b}}--{{key}}--{{value}}</li>
      </ul>
      遍历字符串时，括号中第一个参数是字符串这个位置的值，第二个参数是这个这条遍历的数据的key
      <!-- 遍历字符串 -->
      <ul>
        <li v-for="(value,key) in str">{{key}}--{{value}}</li>
      </ul>
      

...
 data: {
          persons: [
            { id: "001", name: "ice", age: "13" },
            { id: "002", name: "peach", age: "12" },
          ],
          car: {
            speed: "20km/h",
            year: "2014",
          },
          str: "i am a word",
        },
```


展示效果：![img](https://img-blog.csdnimg.cn/8f4801beaac34ab296556baf10b4faf2.png)
 我们要求，每一个遍历的数据都需要一个独有的key，在第一个例子中，可以这样写

```java
<ul>
        <li v-for="(person,index) in persons" :key="person.id">
         {{index}}--{{person.name}}--{{person.age}}
        </li>
      </ul>
```

也可以直接写：key=“index”,这就代表默认的索引就是我们要的key
 具体关于key的下一节讲

遍历指定次数：

```java
<ul>
        <li v-for="(number,index) in 5" :key="index">
         {{number}}--{{index}}
        </li>
      </ul>
```


![img](https://img-blog.csdnimg.cn/75312af0fc254fd38c16efc1c89f8ca5.png)

#### 1.10.2 key的原理和使用

面试题：react、vue中的key有什么作用？(key的内部原理)


1. 虚拟D0M中key的作用：
    key是虚拟DoM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DoM】,
    随后Vue进行【新虚拟DoM】与【旧虚拟DoM】的差异比较，比较规则如下：
<li>对比规则：
    (1).旧虚拟DoM中找到了与新虚拟DoM相同的key:
    a.若虚拟D0M中内容没变，直接使用之前的真实D0M!
    b.若虚拟D0M中内容变了，则生成新的真实D0M,随后替换掉页面中之前的真实D0M。
    (2).旧虚拟DoM中未找到与新虚拟DoM相同的key
    创建新的真实DOM,随后渲染到到页面。</li>
<li>用index作为key可能会引发的问题：
    1,若对数据进行：逆序添加、逆序删除等破坏顺序操作：
    会产生没有必要的真实D0M更新==&gt;界面效果没问题，但效率低。
    2.如果结构中还包含输入类的D0M:
    会产生错误D0M更新=&gt;界面有问题。</li>
<li>开发中如何选择key?:
    1.最好使用每条数据的唯一标识作为key,比如id、手机号、身份证号、学号等唯一值。
    2.如果不存在对数据的逆序添加、逆序刚除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的。![img](https://img-blog.csdnimg.cn/2798684230a744b4a78324b16c496307.png)</li>

#### 1.10.3 列表过滤（查询效果）



实现如下效果：![img](https://img-blog.csdnimg.cn/724a75a704144227b071238a8ce0a8c2.png)![img](https://img-blog.csdnimg.cn/af144456465441a5ba73afae8ad035e1.png)
 两种方法：
 1watch监视：
 注意点：

1. 使用一个数组persnsOfSearch来接受过滤后返回的值
2. 在watch中添加一个immediate，已确保一开始的时候就运行一次watch来显示数据
3. indexOf显示方法参数在字符串中第一次出现的索引，不存在的返回-1，如果方法参数是''空字符串，返回0

```java
<body>
    <div id="root">
        <label>姓名：</label><input v-model="name">
        <ul>
            <li v-for="(person) in persnsOfSearch">
                {{person.name}}--{{person.age}}
            </li>
        </ul>
    </div>
</body>
<script type="text/javascript">

    var vm = new Vue(
        {
            el: '#root',
            data: {
                name: '',
                persnsOfSearch: [],
                persons: [{ id: '001', name: 'ice', age: '17' }, { id: '002', name: 'ipeach', age: '18' }, { id: '003', name: 'icepeach', age: '19' }]
            },
            watch: {
                name: {
                    immediate: true,
                    handler(newValue, oldValue) {
                        this.persnsOfSearch= this.persons.filter((p) => {
                            return p.name.indexOf(newValue) != -1
                        })
                    },
                }
            }
        }
    )

</script>
```

使用计算属性实现：

```java
<body>
    <div id="root">

        <label>姓名：</label><input v-model="name">
        <ul>
            <li v-for="(person) in persnsOfSearch">
               {{person.name}}--{{person.age}}
            </li>
        </ul>
    </div>
</body>
<script type="text/javascript">

    var vm = new Vue(
        {
            el: '#root',
            data: {
                name:'',
                
                persons: [{ id: '001', name: 'ice', age: '17' }, { id: '002', name: 'ipeach', age: '18' }, { id: '003', name: 'icepeach', age: '19' }]
            },
            computed:{
                persnsOfSearch(){
                    return this.persons.filter((p) => {
                            return p.name.indexOf(this.name) != -1
                        })
                } 
            }
        }
    )

</script>
```

可以看到，使用computes明显要更简单一些，所以当computed和watch都可以实现某个功能时，使用computed更好一些

#### 1.10.4 排序

还是在computed中排序
 注意点：


1. 在计算属性中，先过滤，后排序，把过滤好的数据暂时存到一个数组中，然后排序，再返回
2. 使用sort(a,b)的方法来排序：
    若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
    若 a 等于b，则返回 0。
    若 a 大于 b，则返回一个大于 0 的值。
    简单点就是：比较函数两个参数a和b，返回a-b 升序，返回b-a 降序
    效果：![img](https://img-blog.csdnimg.cn/ccdd95362917472e9feeb44355a966ea.png)

```java
<body>
    <div id="root">

        <label>姓名：</label><input v-model="name">
        <button @click="sortType = 0">原顺序</button>
        <button @click="sortType = 1">降序</button>
        <button @click="sortType = 2">升序</button>
        <ul>
            <li v-for="(person) in persnsOfSearch">
                {{person.name}}--{{person.age}}
            </li>
        </ul>

    </div>
</body>
<script type="text/javascript">

    var vm = new Vue(
        {
            el: '#root',
            data: {
                name: '',
                sortType: 0,//0 原顺序 1 降序 2 升序
                persons: [{ id: '001', name: 'ice', age: '17' }, { id: '002', name: 'ipeach', age: '18' }, { id: '003', name: 'icepeach', age: '19' }]
            },
            computed: {
                persnsOfSearch() {
                    const arr = this.persons.filter((p) => {
                        return p.name.indexOf(this.name) != -1
                    })
                    if (this.sortType) {
                        arr.sort((p1, p2) => {
                            return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
                        })
                    }
                    return arr;
                }
            }
        }
    )

</script>
```

#### 1.10.5 监视数据改变的原理

Vue监视数据的原理：

1. vue会监视data中所有层次的数据。
2. 如何监测对象中的数据
    通过setter实现监视，且要在new Vue时就要传入要检测的数据
    (1).对象中后追加的属性，Vue默认不做响应式处理
    (2).如需给后添加的属性做响应式，请使用如下API:
    Vue.set(target,propertyName/index,value)或者
    vm.$set(target,propertyName/index,value)
<li>如何监测数组中的数据？
    通过包裹数组更新元素的方法实现，本质就是做了两件事：
    (1).调用原生对应的方法对数组进行更新。
    (2).重新解析模板，进而更新页面。</li>
<li>在Vue修改数组中的某个元素一定要用如下方法：
    1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
    2.Vue.set()或者vm.s e t ( ) 特别注意： V u e . s e t ( ) 和 v m . set() 特别注意：Vue.set()和vm. set()特别注意：Vue.set()和vm.set()不能给vm或vm的根数据对象添加属性！！</li>

### 1.11 获取表单数据

朋友们，这个很简单，我直接上总结了
 还可以参考官方这部分教程，例子要全一些： [表单输入绑定](https://v2.cn.vuejs.org/v2/guide/forms.html)
 收集表单数据：

1. ,则v-model收集的是value值，用户输入的就是value值。
2. ,则v-model收集的是value值，且要给标签配置value值。
3. 

1.没有配置input的value属性，那么收集的就是checked(勾选or未勾选，是布尔值)
 2.配置input的value属性：
 (1)v-model的初始值是非数组，那么收集的就是checked(勾选or未勾选，是布尔值)
 (2)v-mode1的初始值是数组，那么收集的的就是va1ue组成的数组

备注：v-mode1的三个修饰符：
 1azy:失去焦点再收集数据
 number:输入字符串转为有效的数字
 trim:输入首尾空格过滤

### 1.12 过滤器

过滤器在vue3中已经被取消了，而且过滤器能实现的功能，computed，methods之类的基本都能实现，所以简单概括
 过滤器：
 定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
 语法：

1. 注册过滤器：Vue.filter(name,callback)或new Vue{filters:({}】
2. 使用过滤器：{<!-- -->{xxx|过滤器名}}或v-bind:属性=“xxx | 过滤器名”
    备注
3. 过滤器也可以接收额外参数、多个过滤器也可以串联
4. 并没有改变原本的数据，是产生新的对应的数据

### 1.13 内置指令

#### 1.13.1 v-text

我们学过的指令：
 v-bind:单向绑定解析表达式，可简写为：xxx
 v-mode:双向数据绑定
 v-for：遍历数组/对象/字符串
 v-on：绑定事件监听，可简写为
 v-if：条件渲染（动态控制节点是否存存在）
 v-else：条件渲染（动态控制节点是否存存在）
 v-show:条件渲染（动态控制节点是否展示）
 v-text指令：
 1.作用：向其所在的节点中谊染文本内容。
 2.与插值语法的区别：V-text会替换掉节点中的内容，{<!-- -->{xx}}则不会。

#### 1.13.2 v-html指令

1.作用：向指定节点中谊染包含html结构的内容。
 2.与插值语法的区别
 (1).v-html会替换掉节点中所有的内容，{<!-- -->{xx}}则不会.
 (2).v-html可以识别html结构.
 3.严重注意：v-htm1有安全性问题！！！！
 (1).在网站上动态渲染任意HTML是常危险的，容易导致XSS政击。
 (2).一定要在可信的内容上使用v-html,永不要用在用户提交的内容上！

#### 1.13.3 v-cloak指令

v-cloak指令（没有值）：

1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性.
2. 使用css配合v-cloak可以解决网速慢时页面展示出{<!-- -->{xx}}的问题。

```java
<style>
[v-cloak]{
dispaly:none
}
</style>
...
<h2 v-cloak>{{}}</h2>
```

#### 1.13.4 v-once

需求：如果我们想要展示某一个数据的初识值，即使数据被改变也只展示初识值，就可以使用v-once

```java
<h1 v-once>{{time}}</h1>
```


![img](https://img-blog.csdnimg.cn/77b1af8ca7ae443c9f7f732a01e5478f.png)

1. v-once所在节点在初次动态渲染后，就视为静态内容了。
2. 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

### 1.13.5 v-pre指令

1.跳过其所在节点的编译过程。
 2.可利用它跳过过没有使用指令语法、没有使用插值语法的节点，会加快编译。

就是说标签上加了这个之后，就不会再编译这一个标签了,所以只要我们用到了插值，指令就不要用这个

```java
<h2 v-pre>你好</h2>
<h2 v-pre>当前的值是：{{n}}</h2>
```


![img](https://img-blog.csdnimg.cn/8045707cb3cb4f63a111f10b4e1d807a.png)

#### 1.13.6 自定义指令


各位好啊，自定义指令的教程较为复杂，我有些犯懒了，这里就直接贴上老师的笔记了：![img](https://img-blog.csdnimg.cn/4bd1a9f43c5141078b9d560962b0985b.png)

### 1.14 生命周期




分开的截图（为了让您看的更清晰一些）：![img](https://img-blog.csdnimg.cn/d54e4d8f86234f9ea76013389a7ba743.png)![img](https://img-blog.csdnimg.cn/f9672ea505f54577b84556e20730e264.png)
 完整图：![img](https://img-blog.csdnimg.cn/f92274f0cd994e05a808f0487e340748.png#pic_center)

首先生命周期说的是Vue的生命周期而不是vm的生命周期
 vm的一生(vm的生命周期)：
 将要创建===>调用beforeCreatei函数。
 创建完毕===>调用created函数。
 将要挂载===>调用beforeMount函数。
 (重要)挂载完毕===>调用mountedi函数。=======>【重要的钩子】
 将要更新===>调用beforeUpdatei函数。
 更新完毕===>调用updated函数。
 (重要)将要销毁===>调用beforeDestroyi函数。=====&gt;【重要的钩子】
 销毁完毕==>调用destroyed函数。

人生最重要的时刻：出生（mounted时候，我们一上来要做的事情都放在这）和将要离开的时候（beforeDestory 关闭你以前订阅的消息，关闭定时器，删除浏览记录之类的）

## 2 组件

好耶，我们终于进入第二章了！前面学了那么久，竟然还只是第一张，我真的栓Q，还好坚持到现在。
 学完组件，就开始学脚手架了，激动的嘞~

我们要搞懂，什么是组件，为什么要用组件

### 2.1 模块和组件，模块化和组件化


传统的写页面的方式：
 写html，写css，写js，然后写新的页面时，复制相同的css，js代码，再加上自己的代码![img](https://img-blog.csdnimg.cn/e4552a181b25402f8b40870a52674924.png)**2023**了，谁还用传统方式编程啊（md，我就是）

模块：

1. 理解：向外提供特定功能的js程序，一般就是一个js文件
2. 为什么：js文件很多很复杂
3. 作用：复用js,简化js的编写，提高js运行效率

组件：

1. 理解：用来实现局部特定)功能效果的代码集合(html/css/js/image.)
2. 为什么：一个界面的功能很复杂
3. 作用：复用编码，简化项目编码，提高运行效率

模块化：当应用中的js都以模块来编写的，那这个应用就是一个模块化的应用。

组件化：当应用中的功能都以组件的方式来编写，那这个应用就是一个组件化的应用。

### 2.2 非单文件组件

#### 2.2.1 基本使用

创建组件的api：Vue.extend({})
 大括号里面，几乎和我们之前写vm一样，该data就data，该methods就methods
 但是不能用el哦

Vue中使用组件的三大步骤：
 一、 定义组件（创建组件）
 二、 注册组件
 三、 使用组件（写组件标签）
 一、如何定义一个组件？
 使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别：
 区别如下：

1. el不要写，为什么？
    最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
<li>data必须写成函数，为什么？
    避免组件被复用时，数据存在引用关系。
    备注：使用template可以配置组件结构。
    二、如何注册组件？
    1.局部注册：靠new Vue的时候传入components选项(只在这一个实例里生效)
    2.全局注册：靠Vue.component(‘组件名’，组件)
    三、
    编写组件标签：</li>

```java
<body>
		
		<div id="root">
			<hello></hello>
			<hr>
			<h1>{{msg}}</h1>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<school></school>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<student></student>
		</div>

		<div id="root2">
			<hello></hello>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		//第一步：创建school组件
		const school = Vue.extend({
			template:`
				<div class="demo">
					<h2>学校名称：{{schoolName}}</h2>
					<h2>学校地址：{{address}}</h2>
					<button @click="showName">点我提示学校名</button>	
				</div>
			`,
			// el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
			data(){
				return {
					schoolName:'江南大学',
					address:'无锡'
				}
			},
			methods: {
				showName(){
					alert(this.schoolName)
				}
			},
		})

		//第一步：创建student组件
		const student = Vue.extend({
			template:`
				<div>
					<h2>学生姓名：{{studentName}}</h2>
					<h2>学生年龄：{{age}}</h2>
				</div>
			`,
			data(){
				return {
					studentName:'桃桃',
					age:18
				}
			}
		})
		
		//第一步：创建hello组件
		const hello = Vue.extend({
			template:`
				<div>	
					<h2>你好啊！{{name}}</h2>
				</div>
			`,
			data(){
				return {
					name:'Tom'
				}
			}
		})
		
		//第二步：全局注册组件
		Vue.component('hello',hello)

		//创建vm
		new Vue({
			el:'#root',
			data:{
				msg:'你好啊！'
			},
			//第二步：注册组件（局部注册）
			components:{
				school,
				student
			}
		})

		new Vue({
			el:'#root2',
		})
	</script>
```

#### 2.2.2 注意项

几个注意点：

1. 关于组件名:
    一个单词组成：
    第一种写法(首字母小写)：school
    第二种写法(首字母大写)：School
    多个单词组成：
    第一种写法(kebab-case命名)：my-school
    第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持)
    备注：
    (1).组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。
    (2).可以使用name配置项指定组件在开发者工具中呈现的名字。

```java
//定义组件
		const s = Vue.extend({
			name:'peach',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			}
		})
```

之后，开发者工具中显示的名字就是peach了
 2. 关于组件标签:
 第一种写法：<school></school>
 第二种写法：<school/>
 备注：不用使用脚手架时，会导致后续组件不能渲染。

1. 一个简写方式：
    const school = Vue.extend(options) 可简写为：const school = options

#### 2.2.3 嵌套组件

实际上，嵌套组件就是前两节的使用，只不过是在创建一个组件时，本身再添加之前创建的组件，没有什么其他的东西，很多同学觉得困难，是因为前两节没学好

```java
<body>
		<!-- 准备好一个容器-->
		<div id="root">
			
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		//定义student组件
		const student = Vue.extend({
			name:'student',
			template:`
				<div>
					<h2>学生姓名：{{name}}</h2>	
					<h2>学生年龄：{{age}}</h2>	
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					age:18
				}
			}
		})
		
		//定义school组件
		const school = Vue.extend({
			name:'school',
			template:`
				<div>
					<h2>学校名称：{{name}}</h2>	
					<h2>学校地址：{{address}}</h2>	
					<student></student>
				</div>
			`,
			data(){
				return {
					name:'尚硅谷',
					address:'北京'
				}
			},
			//注册组件（局部）
			components:{
				student
			}
		})

		//定义hello组件
		const hello = Vue.extend({
			template:`<h1>{{msg}}</h1>`,
			data(){
				return {
					msg:'欢迎来到尚硅谷学习！'
				}
			}
		})
		
		//定义app组件
		const app = Vue.extend({
			template:`
				<div>	
					<hello></hello>
					<school></school>
				</div>
			`,
			components:{
				school,
				hello
			}
		})

		//创建vm
		new Vue({
			template:'<app></app>',
			el:'#root',
			//注册组件（局部）
			components:{app}
		})
	</script>
```

#### 2.2.4 关于VueComponent

1. school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。
2. 我们只需要写或，Vue解析时会帮我们创建school组件的实例对象，
    即Vue帮我们执行的：new VueComponent(options)。
3. 特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！
<li>关于this指向：
    (1).组件配置中：
    data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。
    (2).new Vue(options)配置中：
    data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。</li>
<li>VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）。
    Vue的实例对象，以后简称vm。</li>


实际上 vc和vm是很像的双胞胎![img](https://img-blog.csdnimg.cn/667afa956ce74f799bca05f488a5c173.png)

#### 2.2.5

首先我们要知道一个前置知识:
 这段看不懂的，需要去学一下es6中的高级js知识

```java
<script>
//定义一个构造函数
		 function Demo(){
			this.a = 1
			this.b = 2
		}
		//创建一个Demo的实例对象
		const d = new Demo()
		console.log(Demo.prototype) //显示原型属性
		console.log(d.__proto__) //隐式原型属性
		console.log(Demo.prototype === d.__proto__)
		//程序员通过显示原型属性操作原型对象，追加一个x属性，值为99
		Demo.prototype.x = 99

		console.log('@',d) 
		</script>
```

各位好，为了速成（做项目），我先不看视频了找个笔记去学一下
 看的这个笔记： [笔记地址](http://t.csdn.cn/czoDQ)

### 组件的自定义事件总结：


![img](https://img-blog.csdnimg.cn/977a26305d6242a1917ade416c6167d9.png)

### 全局事件总线


![img](https://img-blog.csdnimg.cn/4496d361faef4add8f37b6c7e1e4eaf4.png)

### 消息订阅


![img](https://img-blog.csdnimg.cn/87b3486a11de4c16b9c5e3bd05b74d78.png)

### axios


![img](https://img-blog.csdnimg.cn/b3b5d3b5d5004e25acd86e68bbaa3373.png)
 上图中2，3都是封装的1，如果1不能用了，2，3就都不能用了。
 然后jQuery的80%内容都在封装dom，剩下的才是封装一些周边的东西，比如$.get,$.post
 然后fetch和xhr是平级的，但是有两个问题，就是它封装了两次promise，所以要then两次才能拿到数据，然后它存在兼容性问题，比如ie浏览器就不可以使用fetch
 综上，我们使用axios


首先，我们写一个axios的get![img](https://img-blog.csdnimg.cn/3f5ed63a50ff44fd95cb3a129a54145b.png)

运行的时候我们发现，哎呀妈呀跨域了，为什么会跨域呢，原因是我们违背了**同源原则****同源原则**：协议名，主机名，端口号
 如下图，端口号对不上

>实际上，我们请求之后，服务器是收到了请求，而且把数据返回了，但是浏览器一看，哎不同源，就把数据藏起来了


![img](https://img-blog.csdnimg.cn/e0d9010878e0497e9cfff832d62ef896.png)


解决方法
 1cors:
 在服务器里，返回数据的时候，添加了一些请求头，然后浏览器一看，你都这么表态了，那我就把数据给你吧。所以在服务器解决跨域问题才是真正的解决跨域![img](https://img-blog.csdnimg.cn/8e5449543c2d42978ca467f2940eb1b1.png)
 2 jsonp
 只能解决get请求的


3 配置代理服务器![img](https://img-blog.csdnimg.cn/01f773b0650d4078b6779def03adad96.png)
 使用方法：1 nginx(有点麻烦) 2 vue-cli


vue-cli:
 添加配置的第一种方法：![img](https://img-blog.csdnimg.cn/f9de45fcceb64da5ab98be4d22cb5c81.png)


vue-cli添加配置的第er二种方法![img](https://img-blog.csdnimg.cn/832533819a044d5a9c7605b94d807745.png)

加上·pathRewrite:{'/atguigu':''的意思是，在把请求中的atguigu去掉




总结:![img](https://img-blog.csdnimg.cn/542276adefc14742ba5e1d95ce3cd877.png)![img](https://img-blog.csdnimg.cn/95768906557846a2b9457616c4a94c3a.png)![img](https://img-blog.csdnimg.cn/19d5d596528c4b889521e7e6b719879d.png)

### vuex


![img](https://img-blog.csdnimg.cn/d357e3baa23f437d9bec64c0a046c254.png)


我们现在用的是vue2，所以要安装vuex3![img](https://img-blog.csdnimg.cn/dcfc8ffc1e1544d6b512da4f3f959bb3.png)

