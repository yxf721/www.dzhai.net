title: Windows下配置Java环境变量
date: 2015-02-13 21:17:39
categories: 环境配置
keywords: dzhai
tags: [WIndows]
---

###环境变量
```
添加环境变量JAVA_HOME
JAVA_HOME=C:\Program Files\Java\jdk1.7.0
添加环境变量CLASSPATH
CLASSPATH=.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
在Path 后面追加内容
Path=%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
```
<!--more-->



