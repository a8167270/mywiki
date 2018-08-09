---
title: "nginx"
date: 2018-08-09 20:31
---

## 安装

```shell
yum install -y nginx
```

## 启动

```shell
service nginx start
```

## 修改配置信息

默认的配置信息的路径一般在`/etc/nginx/nginx.conf`,而配置的文件夹默认路径一般在`/usr/share/nginx/html` 

## 重启

```shell
service nginx reload

service nginx restart
```

## 卸载

```shell
# 先使用yum卸载
yum remove nginx

# 在使用whereis查找遗漏文件
whereis nginx
```

