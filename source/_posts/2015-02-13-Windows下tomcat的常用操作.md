title: Windows下tomcat的常用操作
date: 2015-02-13 21:15:57
categories: 环境配置
keywords: dzhai
tags: [Tomcat,Windows]
---
### 免安装版设置内存
```
在catalina.bat 的首行中添加 如下配置
set JAVA_OPTS=-Xms512m -Xmx512m -XX:PermSize=128m -XX:MaxPermSize=256m
```

### 配置Windows 服务
```
安装服务
service.bat instart
删除服务
service.bat remove

设置windows 服务的JVM参数
1 启动下tomcat服务 查看是否启动成功
2 找到打开tomcat7w.exe-->点击 java tab 
在java Options下添加
-Xms512m
-Xmx512m
-XX:PermSize=128m
-XX:MaxPermSize=256m
每一行后面不能有空格
```
<!--more-->
<!--more-->



