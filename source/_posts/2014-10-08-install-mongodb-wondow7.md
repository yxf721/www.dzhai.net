title: install-mongodb-wondow7
categories: MongoDB
keywords: dzhai
date: 2014-10-08 11:11:31
tags: [MongoDB, NodeJs]
---

##Download MongoDB

There are three builds of MongoDB for Windows:

1) MongoDB for Windows Server 2008 R2 edition [[Download link](https://fastdl.mongodb.org/win32/mongodb-win32-x86_64-2008plus-2.6.1.zip "download mongodb for windows server 2008")] 

2) MongoDB for Windows 64-bit [[Download link](https://fastdl.mongodb.org/win32/mongodb-win32-x86_64-2.6.1.zip "Download mongodb for windows 64 bit")]

3) MongoDB for Windows 32-bit [[Download link](https://fastdl.mongodb.org/win32/mongodb-win32-i386-2.6.1.zip "Download mongodb for windows 32 bit")]

>To find which version of Windows you are running, enter the following command in the Command Prompt:

>c:\&gt; wmic os get osarchitecture

[**More download options**](http://www.mongodb.org/downloads "MongoDB downloads") are given in official website of MongoDB.

##Install MongoDB   

The given links above will download zip files which you extract directly onto any place in your system of your choice. I have extracted them in “`d:/mongodb`“. So, all code samples will in this post as well as future posts will refer to this location.

>It’s recommended to add **d:/mongodb/bin** to Windows environment variable, so that you can access the MongoDB’s commands in command prompt directly.

Also, please **create following directories** inside d:/mongodb

*   D:\mongodb\data
*   D:\mongodb\log

##Create mongo.config Configuration File

This is important step before marching ahead. Create a normal text file in location `d:/mongodb` and save it with name `mongo.config`.

Now place the below configuration options in file. You can change the option’s values at your will.

````
##Which IP address(es) mongod should bind to. 
bind_ip = 127.0.0.1
 
##Which port mongod should bind to.
port = 27017
 
##I set this to true, so that only critical events and errors are logged.
quiet = true
 
##store data here
dbpath=D:\mongodb\data
  
##The path to the log file to which mongod should write its log messages.
logpath=D:\mongodb\log\mongo.log
 
##I set this to true so that the log is not overwritten upon restart of mongod.
logappend = true
  
##log read and write operations
diaglog=3
 
##It ensures write durability and data consistency much as any journaling scheme would be expected to do. 
##Only set this to false if you don’t really care about your data (or more so, the loss of it).
journal = true
```
##Start/Shutdown the MongoDB Server

To **start the MongoDB server**, use below command in command prompt:

> **mongod.exe --config d:\mongodb\mongo.config**
```
D:\mongodb\bin>mongod --config D:\mongodb\mongo.config --journal
2014-05-25T16:51:18.433+0530 warning: --diaglog is deprecated and will be removed in a future release
2014-05-25T16:51:18.434+0530 diagLogging level=3
2014-05-25T16:51:18.435+0530 diagLogging using file D:\mongodb\data/diaglog.5381d22e
```

To **connect to MongoDB** from command prompt, use below command:

> **d:\mongodb\bin&gt;mongo**
```
D:\mongodb\bin>mongo
MongoDB shell version: 2.6.1
connecting to: test
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see   http://docs.mongodb.org/
Questions? Try the support group   http://groups.google.com/group/mongodb-user
Server has startup warnings:
2014-05-25T16:52:09.158+0530 [initandlisten]
2014-05-25T16:52:09.158+0530 [initandlisten] ** NOTE: This is a 32 bit MongoDB binary.
2014-05-25T16:52:09.158+0530 [initandlisten] **       32 bit builds are limited to less than 2GB of data (or less with --jour
nal).
2014-05-25T16:52:09.158+0530 [initandlisten] **       See http://dochub.mongodb.org/core/32bit
2014-05-25T16:52:09.158+0530 [initandlisten]
```

To **shutdown the MongoDB server**, you must be authorized user. So after getting auth complete, use below command in command prompt:

> **db.shutdownServer()**
```
> use admin
switched to db admin
> db.shutdownServer()
2014-05-25T19:55:25.221+0530 DBClientCursor::init call() failed
server should be down...
2014-05-25T19:55:25.224+0530 trying reconnect to 127.0.0.1:27017 (127.0.0.1) failed
2014-05-25T19:55:26.225+0530 warning: Failed to connect to 127.0.0.1:27017, reason: errno:10061 No connection could be made b
ecause the target machine actively refused it.
2014-05-25T19:55:26.225+0530 reconnect 127.0.0.1:27017 (127.0.0.1) failed failed couldn't connect to server 127.0.0.1:27017 (
127.0.0.1), connection attempt failed
> quit()
 
D:\mongodb\bin>
```

##MongoDB Windows Service

To install the window service, use below command:

> **mongod --config D:\mongodb\mongo.config --install**

Start the windows service from command prompt:

> **net start MongoDB**

Stop the windows service from command prompt:

> **net stop MongoDB**

Remove the windows service

> **mongod --remove**

Sample run of all above four commands is below:

```
D:\mongodb\bin>mongod --config D:\mongodb\mongo.config --install
2014-05-25T20:07:41.191+0530 warning: --diaglog is deprecated and will be removed in a future release
2014-05-25T20:07:41.192+0530 diagLogging level=3
2014-05-25T20:07:41.193+0530 diagLogging using file D:\mongodb\data/diaglog.53820035
 
D:\mongodb\bin>net start MongoDB
 
The MongoDB service was started successfully.
 
 
D:\mongodb\bin>net stop MongoDB
System error 109 has occurred.
 
The pipe has been ended.
 
 
D:\mongodb\bin>mongod --remove
2014-05-25T20:09:32.514+0530
2014-05-25T20:09:32.515+0530 warning: 32-bit servers don't have journaling enabled by default. Please use --journal if you wa
nt durability.
2014-05-25T20:09:32.515+0530
2014-05-25T20:09:32.518+0530 Trying to remove Windows service 'MongoDB'
2014-05-25T20:09:32.520+0530 Service 'MongoDB' removed
 
D:\mongodb\bin>
```

##Download/Use MongoDB Java Driver

Download the MongoDB java driver (mongo-java-driver-2.9.3.jar) from this **[download link](http://central.maven.org/maven2/org/mongodb/mongo-java-driver/2.9.3/mongo-java-driver-2.9.3.jar "mongodb java driver download")**. It’s a jar file you need to include in your classpath/ copy in lib folder in project where you want to use MongoDB.

##Verify MongoDB Installation

To verify that MongoDB has been installed and working properly, execute below program:

```java
package examples.mongodb.install;
 
import java.net.UnknownHostException;
import java.util.List;
 
import com.mongodb.MongoClient;
 
public class VerifyMongoDBInstallation {
    public static void main(String[] args) throws UnknownHostException {
        MongoClient mongo = new MongoClient("localhost", 27017);
 
        List<String> dbs = mongo.getDatabaseNames();
        for (String db : dbs) {
            System.out.println(db);
        }
    }
}
 
Output:
 
local
admin
```

That’s all for **MongoDB installation, startup and shutdown operations**. Next, we will learn about some CRUD operations. Follow me to stay tuned.

**Happy Learning !!**
<!--more-->



