---
title: "基本操作"
layout: page
date: 2018-01-02
collection: docker
---
[TOC]

# 基本操作

# 进入docker容器
```
docker exec -t -i dev_tomcat /bin/bash
```

# 拷贝文件

```
docker cp /usr/tmp/working.war ea9e37fb58ec7618cc80af8063171d11fa4b2f77db55f852f904d3cc772d887c:/usr/local/tomcat/webapps
```
