---
title: oracle数据库--从备份文件恢复
date: 2019-09-21 21:07:48
tags: oracle数据库
---

Oracle 数据库 .dpdmp 文件导入数据库

使用命令`impdp system/root DIRECTORY=data_dump_dir DUMPFILE=MYDUMPFILE.DPDMP`

其中`system/root`为对应的用户名和密码，后面两个参数依次是`dump`文件所在目录以及文件名。这个操作要求用户~~民~~具有`DBA`权限。

