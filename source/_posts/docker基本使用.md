---
title: docker基本使用
date: 2019-01-30 08:56:27
tags: docker
---

# docker基本使用

<!-- more -->

<!-- [TOC] -->

## dockerfile编写(待补充)

### dockerfile文件

```
FROM java:8
MAINTAINER SOLASJ
COPY ./sc-registry-0.0.1-SNAPSHOT.jar app.jar
CMD java -jar app.jar
```

### 创建image

```
# -t 指明image的名字, . 代表当前路径
docker build -t app .
```

### 运行image

```
# -p 指明端口映射, -d 后台运行
docker run -p 8761:8761 -d app
```

## 常用命令

### 进入已经运行的容器中

```
docker exec -it [containerId] /bin/bash  
```

### 运行并进入到容器的命令行模式

```
docker run -t -i [image] /bin/bash
```

### 退出容器内部

输入`exit`, 或者`ctrl+d`

### 查看所用容器ip

```
docker inspect -f '{{.Name}} - {{.NetworkSettings.IPAddress }}' $(docker ps -aq)
```

如果是docker-compose则使用以下命令:
```
docker inspect --format='{{.Name}} - {{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $(docker ps -aq)
```
