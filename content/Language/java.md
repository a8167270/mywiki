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

## list 转换为map
```java
Map<City, List<String>> result = Person.stream().collect(Collectors
.groupingBy(Person::getCollege, HashMap::new, Collectors.mapping(Person::getLastName, Collectors.toList())));
```
```java
Map<City, Set<String>> namesByCity = people.stream()
    .collect(groupingBy(Person::getCity, TreeMap::new,mapping(Person::getLastName,toSet())));
```

### List根据另一个List排序

```java
Collections.sort(listB, new Comparator<Item>() {
    public int compare(Item left, Item right) {
        return Integer.compare(listA.indexOf(left), listA.indexOf(right));
    }
});
```

