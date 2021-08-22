---
title: 优选Cloudflare最快IP
date: 2020-11-02 09:12:53
tags: Cloudflare
keywords: Cloudflare
description: 优选Cloudflare
---

套 CF 保命的时候总会遇到网速不快的问题，经实践，可以更换由 CF 提供的默认 IP 来达到提速的目的。



<!--more-->



```python
import requests
import threadpool
from IPy import IP

def IP_Test(ip):
    try:
        r = requests.get('http://' + ip + '/', timeout=3)
        if 'Direct IP access not allowed' in r.text:
            print('可用:' + ip, flush=True)
            with open('cf_ips_full.txt', mode='a') as filename:
                filename.write(ip)
                filename.write('\n') # 换行
        else:
            print('不可用:' + ip, flush=True)
    except requests.exceptions.ConnectionError:
        print('无服务:' + ip, flush=True)
    except requests.exceptions.ReadTimeout:
        print('无服务:' + ip, flush=True)


iplist = list()


cidr=['173.245.48.0/20','103.21.244.0/22','103.22.200.0/22','103.31.4.0/22','141.101.64.0/18','108.162.192.0/18','190.93.240.0/20','188.114.96.0/20','197.234.240.0/22','198.41.128.0/17','162.158.0.0/15','104.16.0.0/12','172.64.0.0/13','131.0.72.0/22']
# cidr6=['2400:cb00::/32','2606:4700::/32','2803:f800::/32','2405:b500::/32','2405:8100::/32','2a06:98c0::/29','2c0f:f248::/32']
for xip in cidr:
    ips = IP(xip)
    for ip in ips:
        iplist.append(str(ip))

pool = threadpool.ThreadPool(10000)  # 线程池设置,最多同时跑N个线程
tasks = threadpool.makeRequests(IP_Test, iplist)
[pool.putRequest(task) for task in tasks]
pool.wait()
```

以上是根据 CF 提供的 CIDR 地址解析出单个 IP 并放到文件中。

由于我用的 Windows 10 所以就没写 shell 脚本，写了个 PowerShell  脚本【注：需要要7.0 以上版本才能运行这个脚本，因为开启了多线程】。

以下就是 PowerShell  脚本，作用是得出上面的 IP 中的 PING 值。

```powershell
Start-Transcript -Path .\cf_full.txt
(Get-Content .\cf_ips_full.txt) | ForEach-Object -ThrottleLimit 24000 -Parallel {
    Write-Host $_',',([System.Net.NetworkInformation.Ping]::new().Send($_)).RoundtripTime
    }
Stop-Transcript
```

这一步的结果出来就要手动选了。

这里我给出联通网络下 PING 值较好的 IP [文件](/images/github/file/below200.csv)。