title: GoAgent和Heroku搭建翻墙
categories: 工具使用
keywords: goagnet
date: 2015-07-12 10:08:34
tags: [goagent, heroku]
---
以前一直使用goagent翻墙 使用gmail或者搜索一些资料，最近goagent使用GAE一直无法访问google，看到goagent支持PHP代理，就萌生了使用免费的空间Heroku 搭建PHP代理，下面介绍下主要步骤。
<!--more-->
### 准备工作
1. 下载最新版 **[goagent3.2.3](https://github.com/goagent/goagent)** 
2. 去**[Heroku](https://dashboard.heroku.com/)**注册一个账号
3. 如果没有**[Github](https://github.com/)**账号的自己注册一个，已经有的跳过
4. Fork资源**[php-getting-started](https://github.com/dzhai/php-getting-started)**到自己的Gitgub账号下
### 创建Heroku APP
1. 进去Heroku 控制面板 https://dashboard.heroku.com/apps 
2. 创建一个APP    

2.1 添加一个APP
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_01.png)    

2.2 设置APP名称
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_02.png)

2.3 选择部署方式 Github
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_03.png)

2.4 选择部署的资源
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_04.png)

2.5 设置部署选项    
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_05.png)

2.6 部署成功  
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_06.png)
### 修改Goagent配置文件
1. 复制Heroku APP访问地址 https://goagentphp.herokuapp.com/
2. 打开goagent配置文件 proxy.ini
3. 修改PHP的设置
```
enable = 1
fetchserver = https://goagentphp.herokuapp.com/1/index.php
```
![](http://7xjq6x.com1.z0.glb.clouddn.com/20150712/heroku_08.png)

### 配置Chrome浏览器插件
1. 安装chrome浏览器插件 请看Goagen 官方介绍 [gogent wiki](https://github.com/goagent/goagent/blob/wiki/InstallGuide.md)
注意证书的安装
2. 使用Goagent PHP代理

### 我配置的Goagent 
1. 下载地址 http://pan.baidu.com/s/1hq4GZ7u
2. 经过本人测试在youtube上看视频微卡，最好改改Heroku的代理路径，人多卡


### link
1. [Github](https://github.com)
2. [Goagent Wiki](https://github.com/goagent/goagent)
3. [Heroku](https://dashboard.heroku.com)



