---
title: "Java 工具"
layout: page
date: 2017-06-01
collection: Java
---
[TOC]

## 列表使用符号连接

```java
//使用','连接list
String a = String.join(",", list;
```

## mapper读取JsonArray

```java
JavaType javaType = mapper.getTypeFactory().constructParametricType(ArrayList.class, String.class);
List<String> mapper.readValue(configStr, javaType);
```