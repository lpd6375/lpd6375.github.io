---
title: notes of daliy use
date: 2020-01-20 17:09:45
tags: mynotes Linux
keywords:
description:
---

Scripts that been used frequently.

常用脚本：



<!--more-->



Issue a ssh key 

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Issue cert:

```bash
curl https://get.acme.sh | sh
```

Or:

```bash
wget -O -  https://get.acme.sh | sh
```

Renew the certs:

```shell
acme.sh --renew -d example.com --force
```

Upgrade:

```bash
acme.sh --upgrade
acme.sh --upgrade --auto-upgrade
```

生成 pem 文件：

```bash
cat fullchain.cer domain.key >> domain.pem
```

V2ray:

```bash
bash <(curl -L -s https://install.direct/go.sh)
```

Shadowsocks:

```text
https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
```

Git:

```shell
git config --global http.proxy socks5://127.0.0.1:10086

git config --global https.proxy socks5://127.0.0.1:10086

git config --global --unset http.proxy

git config --global --unset https.proxy

git config --global user.email "xxx@xx.com"

git config --global user.name  "xxx"

```

Repository Config For SSH:

```text
[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[remote "origin"]
	url = git@github.com:xxx/xxx.github.io.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "all"]
	remote = origin
	merge = refs/heads/all
```

上面的配置中，url 决定了使用哪种方式与git仓库进行连接。

**SSH 设置别名**

以下配置可以实现 `ssh xxx`直接登录服务器。

```yaml
Host aliasofyourserver
    HostName YOURIP
    User username
    Port port
    IdentityFile /path/to/your/private_key

```

