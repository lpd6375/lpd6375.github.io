---
title: 升级所有 Python 包
date: 2021-04-03 17:32:23
tags: technique
keywords: python 脚本
description: 有时候你就是想一键升级所有的包是不是？我也是，搜到了，记录一下
---

运行以下代码即可。其实还是调用



<!--more-->



```python
import pip 
from subprocess import call
from pip._internal.utils.misc import get_installed_distritutions
for x in get_installed_distritutions():
    call("pip install --upgrade "+x.project_name,shell=True)
```

