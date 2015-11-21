title: ConOS6.5  安装Oracle JDK 和 Tomcat
categories: 环境配置
tags:
  - JDK
  - Tomcat
  - CenOS
keywords: Tomcat CenOS
date: 2014-12-17 09:54:39

---
##安装JDK

###下载Oracle JDK 1.7
[点击下载tag.gz文件](http://www.oracle.com/technetwork/java/javase/downloads/index.html)   

###复制到 /opt目录 下并解压
```
/*复制*/
# cp jdk-7u71-linux-x64.tar.gz /opt/

/*解压*/
# tar -zxvf jdk-7u71-linux-x64.tar.gz
```

###配置全局环境变量
 在 `/etc/profile`文件 内追加以下内容
 
``` 
# jdk7 settings
JAVA_HOME=/opt/jdk1.7.0_71
JRE_HOME=$JAVA_HOME/jre
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH
```
然后执行 `source /etc/profile` 使配置生效。

###在 /sbin目录 下建立java的软链接
此时我们在shell中输入java命令，将提示/usr/bin中找不到java命令，那是因为我们还没为$JAVA_HOME/bin/java在/sbin目录下建立软链接
```  
ln -s /opt/jdk1.7.0_71/bin/java /sbin/java
```
到这里Oracle JDK1.7的安装已完成了！

##安装Tomcat7

###下载并解压到 /opt目录 下
[点击下载 tar.gz](http://archive.apache.org/dist/tomcat/tomcat-7/)

###在 `catalina.sh`文件 最顶添加如下内容
``` 
export TOMCAT_HOME=/opt/apache-tomcat-7.0.55
export CATALINA_HOME=/opt/apache-tomcat-7.0.55
export JRE_HOME=/opt/jdk1.7.0_71/jre
export JAVA_HOME=/opt/jdk1.7.0_71
```

###让tomcat开机启动
编辑 /etc/rc.d/rc.local
```
$ sudo vi /etc/rc.d/rc.local 
```
加入如下内容：
```
export JAVA_HOME=/usr/local/jdk1.7.0_71 
/opt/apache-tomcat-7.0.55/bin/startup.sh   
```
###设置Tomcat 内存大小
要添加在tomcat 的bin 下catalina.sh 里，位置cygwin=false前 。注意引号要带上
```
OS specific support. $var _must_ be set to either true or false.
JAVA_OPTS='-Xms1024m -Xmx1024m -Xss1024K -XX:PermSize=256M -XX:MaxNewSize=512m -XX:MaxPermSize=256m'
cygwin=false
```
---
###Link
http://www.cnblogs.com/fsjohnhuang/p/3989418.html
http://blog.csdn.net/zhngjan/article/details/25223423
http://blog.csdn.net/fengyie007/article/details/1780375
http://blog.csdn.net/fengyie007/article/details/1776257
<!--more-->
