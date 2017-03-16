---
layout: post
title: Exception:javax.persistence.Table.indexes()
tags: Exception,Apusic,金蝶
grammar_cjkRuby: true
---

[toc]

## 问题描述

由于项目需要,必须将项目部署到国产中间件Apusic应用服务器中.在启动容器时报
找不到方法: ==javax.persistence.Table.indexes()==

```java
Caused by: java.lang.NoSuchMethodError: javax.persistence.Table.indexes()[Ljavax/persistence/Index;
	at org.hibernate.cfg.annotations.EntityBinder.processComplementaryTableDefinitions(EntityBinder.java:936)
	at org.hibernate.cfg.AnnotationBinder.bindClass(AnnotationBinder.java:824)
	at org.hibernate.cfg.Configuration$MetadataSourceQueue.processAnnotatedClassesQueue(Configuration.java:3788)
	at org.hibernate.cfg.Configuration$MetadataSourceQueue.processMetadata(Configuration.java:3742)
	at org.hibernate.cfg.Configuration.secondPassCompile(Configuration.java:1410)
	at org.hibernate.cfg.Configuration.buildSessionFactory(Configuration.java:1844)
	at org.hibernate.cfg.Configuration.buildSessionFactory(Configuration.java:1928)
	at org.springframework.orm.hibernate4.LocalSessionFactoryBuilder.buildSessionFactory(LocalSessionFactoryBuilder.java:343)
	at org.springframework.orm.hibernate4.LocalSessionFactoryBean.buildSessionFactory(LocalSessionFactoryBean.java:431)
	at org.springframework.orm.hibernate4.LocalSessionFactoryBean.afterPropertiesSet(LocalSessionFactoryBean.java:416)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1612)
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1549)
	... 49 more
```

项目之前在tomcat服务器中能够正常启动.从网上查找资料,很多人说是Hibernate的bug,经过不断的尝试与排查,最终确定这个异常不是Hibernate的bug.

## 解决过程

### 网上解决方案

源代码的编写形式如下所示:

```java 
  @Entity  
  @Table(name = "category")  
  public class Category  {  
  	 // Fields  
 	 private Integer id;  
  	 private String type;  
 	 private Boolean hot;  
  	 //省略  
  }
```

将 ==@Table(name="TABLENAME")== 改写为 ==@Entity(name="TABLENAME")== 这种形式.
这种修改不一定起作用

### 问题的原因

从提示的错误信息来看,问题的原因在 ==javax.persistence.Table== 这个类没有indexes()方法.

### 解决的过程

首先,搜索项目中有哪些包有 ==javax.persistence.Table== 这个类.
搜索结果发现hibernate-jpa和javax.persistence包中有相应的类.

经检查发现 ==javax.persistence-2.0.0== 包中的



## 总结

## 参考资料
