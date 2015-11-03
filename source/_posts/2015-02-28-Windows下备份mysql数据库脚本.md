title: Windows下备份mysql数据库脚本
categories: 环境配置
keywords: Windows,mysql
date: 2015-02-28 10:08:34
tags: [Windows,mysql]
---

###直接上bat
```
@echo off
set yMd=%date:~,4%-%date:~5,2%-%date:~8,2%_
set HH=%TIME:~0,2%
if %TIME:~0,2% leq 9 (set HH=0%TIME:~1,1%)else set HH=%TIME:~0,2%
set mmss=-%TIME:~3,2%-%TIME:~6,2%
set datetime=%yMd%%HH%%mmss%
"D:\Program Files\MySQL\MySQL Server 5.6\bin\mysqldump" --opt -u root --password=root dzhaidb > D:\db_bak\baibaydb\dzhaidb_%datetime%.sql
@echo on
```
###Note   
先在cmd命令中看看自己系统日期的格式化 **date** 和 **time**




