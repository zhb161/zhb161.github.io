---
title: Mybatis-plus中，在新增或修改时，自动插入或修改某个字段值
date: 2023-06-01 09:46:01
author: ice
tags:
- springboot
- java
- mybatis-plus
categories:
- 从头创建一个新项目可能需要的配置
---



# 一 效果

在新增User表的数据时，createTime为null

![image-20230531133204052](https://icepeachpicture.oss-cn-shanghai.aliyuncs.com/ice/b937d4d9b00ab747b9224b0d665d5dc0.png)

使用mybatis-plus自带的save方法新增后，在数据库中有自动插入的当前时间的值

![image-20230531133418819](https://icepeachpicture.oss-cn-shanghai.aliyuncs.com/ice/b38d9729833e7ebbfc80ab60f5393a6a.png)

# 二 实现原理

> ##  MetaObjectHandler:元数据对象处理器

说明:`MetaObjectHandler接口`是mybatisPlus为我们提供的的一个扩展接口，我们可以利用这个接口在我们`插入`或者`更新`数据的时候，`为一些字段指定默认值`。

> 使用场景：公共字段填充，如updateTime、createTime、createUser、updateUser等公共字段的填充。

# 三 使用步骤

## 1 在实体类的公共字段上添加@TableField注解

1. `@TableField(fill = FieldFill.INSERT)`：表示此字段只在插入/新增操作时更新数据；
2. `@TableField(fill = FieldFill.INSERT_UPDATE)`：表示此字段在新增和修改操作时都更新数据；
3. `@TableField(fill = FieldFill.UPDATE)`：表示此字段只在修改操作时更新数据；

如下面代码中，createTime，updateTime，createUser都会在新增时更新数据，updateTime还会在修改时更新数据

```java
@TableName(value = "article")
@Data
public class Article implements Serializable {
    /**
     * id
     */
    @TableId(type = IdType.ASSIGN_UUID)
    private String id;
    /**
     * 图片地址
     */
    private String pictureUrl;
    /**
     * 标题
     */
    private String title;
    /**
     * 创建时间
     */
    @TableField(fill = FieldFill.INSERT)
    private String createTime;
    /**
     * 修改时间
     */
    @TableField(fill = FieldFill.INSERT_UPDATE)
    private String updateTime;

    /**
     * 创建人
     */
    @TableField(fill = FieldFill.INSERT)
    private String createUser;

    @TableField(exist = false)
    private static final long serialVersionUID = 1L;
}
```

## 2 创建配置类实现`MetaObjectHandler`接口

实现`MetaObjectHandler`接口，重写insertFill、updateFill方法

使用接口中的setFieldValByName方法，找到我们之前的几个字段，并给字段赋值

> 不要忘记@Component 注解

如下代码：

```java
@Component
public class MyMetaObjectHandler implements MetaObjectHandler {
    @Override
    public void insertFill(MetaObject metaObject) {
        this.setFieldValByName("createTime", new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date()), metaObject);
        this.setFieldValByName("updateTime", new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date()), metaObject);    
        this.setFieldValByName("createUser", currrentUser.getNickname(), metaObject);
    }

    @Override
    public void updateFill(MetaObject metaObject) {
        this.setFieldValByName("updateTime", new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date()), metaObject);

    }
}
```



