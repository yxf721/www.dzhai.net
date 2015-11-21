title: Nodejs http-server 配置
categories: Nodejs
tags:
  - Nodejs
keywords: Nodejs http-server 配置
date: 2015-11-21 16:05:49
---

1. [下载Nodejs](https://nodejs.org/en/)
2. 按照http-server 组件 打开cmd命令行 执行命令 `npm install http-server -g`
3. 在eclipse中导入svn项目static
4. 将下面内容保存成nodejs_http-server.bat 文件
```  
http-server E:\EWorkSpace\web.resource\static\src -a 192.168.0.128 -p 8181
```
5. 配置nodejs_http-server.bat 文件执行信息
`http-server [部署root目录] -a [ip地址] -p [端口]`

详情参考 [http-server](https://www.npmjs.com/package/http-server)


