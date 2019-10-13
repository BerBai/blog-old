---
layout:     post
title:      Nginx 命令
subtitle:   Windows下Nginx的启动、停止等命令
date:       2019-03-03
author:     涂诣
header-img: img/post-bg-nginx.png
catalog: true
tags:
    - nginx
---

## Windows下Nginx的启动、停止等命令

在Windows下使用Nginx，我们需要掌握一些基本的操作命令，比如：启动、停止Nginx服务，重新载入Nginx等，下面我就进行一些简单的介绍。

### 1、启动：

C:\server\nginx-1.0.2>start nginx或
C:\server\nginx-1.0.2>nginx.exe

### 2、停止：

C:\server\nginx-1.0.2>nginx.exe -s stop或
C:\server\nginx-1.0.2>nginx.exe -s quit

>注：stop是快速停止nginx，可能并不保存相关信息；quit是完整有序的停止nginx，并保存相关信息。

### 3、配置文件修改重新载入Nginx：

C:\server\nginx-1.0.2>nginx.exe -s reload
当配置信息修改，需要重新载入这些配置时使用此命令。

### 4、重新打开日志文件：

C:\server\nginx-1.0.2>nginx.exe -s reopen

### 5、查看Nginx版本：

C:\server\nginx-1.0.2>nginx -v

### 6、验证配置是否正确: 

C:\server\nginx-1.0.2>nginx -t

### 7.查看是否启动成功：

C:\server\nginx-1.0.2>tasklist /fi "imagename eq nginx.exe"