---
title: MYSQL技巧
date: 2019-11-13 14:15:38
tags: 技术
keywords: 
description:
---

这里记录`MySQL`使用过程，经常遇到的问题的解决方案（不涉及高级较高级的操作）。



<!--more-->



1. 如何将数据库从一台服务器移动到另一台服务器？

   ```mysql
   mysqldump -uuser -ppassword myDatabase | mysql -hremoteserver -uremoteuser -premoteserverpassword 
   ```

    下面的这个更详细。

   ```
   mysqldump -h 'xxx.x.x.x' -uTHATUSER -pTHATPWD --opt --compress THATDB --skip-lock-tables | mysql -h localhost -uMYUSER -pMYPWD MYDB
   ```

   这里使用了管道操作。这是一种在线方式，前面的`mysqldump` 用来把指定的数据库导出，管道操作将导出的数据作为输入导入到后面的数据库里。