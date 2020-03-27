---
title: Try on BCH
date: 2020-03-26 19:45:31
tags: Cloud 
keywords: 百度云 BCH
description: 使用BCH 踩的坑
---

本文主要记录使用BCH时踩到的坑。



<!--more-->



> 证书坑
>
> > 配置证书时的坑，由于使用了 Let's encrypt 的自签名证书在配置的时候着实费了少时间。**解决方法是服务器证书填生成的证书包里的fullchain.cer,私钥部分填key结尾的那个**
> >
> 

> 重定向的坑
>
> > wordpress中配置了https后发现在登录时浏览器会返回重定向过多问题。还有就是页面会出现加载不完整的问题，浏览器控制台出现403错误，这是由于wordpress中有部分资源不没有用https方式请求导致。**解决方法是将如下代码加进wp-config.php中即可。**
> >
> > ```php
> > $_SERVER['HTTPS'] = 'on';
> > define('FORCE_SSL_LOGIN', true);
> > define('FORCE_SSL_ADMIN', true);
> > ```
> >

以上就是使用BCH过程中遇到的坑，希望有缘人能搜到这个解决你的问题。还可以用邮箱联系我

admin@stupromo.com

