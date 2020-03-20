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

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Issue cert:

```
curl https://get.acme.sh | sh
```

Or:

```
wget -O -  https://get.acme.sh | sh
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

```
git config --global https.proxy http://127.0.0.1:10086

git config --global https.proxy https://127.0.0.1:10086

git config --global --unset http.proxy

git config --global --unset https.proxy
```

