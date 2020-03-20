---
title: 利用 Cloudflare 实现端口映射
date: 2019-10-28 21:28:40
tags: 技术
keywords:
description:
---

新装的宽带给了公网IP刚好光猫上也有虚拟服务器功能，于是乎想到了要搞一个端口映射的东西。由于使用的是windows 所以自然选择了powershell 作为驱动脚本。上海电信 80、8080、443 端口是完全不给的，其它一率开放。



<!--more-->



简单解释一下思路，首先是获取本地的外网 IP 地址，然后把 CF 上的解析记录改一下。在此之前要先在 CF 上设置对应的解析记录。因为这里调用的是 CF 的更新记录 API。 为保证服务的持续有效，设置了一个十分钟的检查，这个可以设置成更短的时间，但是由于DNS生效可能需要一点时间，具体的参数值，自己摸索吧。

```powershell
$getip = Invoke-WebRequest iiip.co
$iip = $getip.Content.Trim()
$apitoken = 'xxxx'
$zoneId = 'xxxx'
$url ="https://api.cloudflare.com/client/v4/zones/"+$zoneId+"/dns_records?type=A&name=domain.domain.xxx&match=all"
$headers = @{"Authorization"="bearer "+$apitoken}
$contentype = "application/json"
while(1){
    $out = Invoke-WebRequest -Uri $url -Headers $headers -ContentType $contentype
    $dataa = $out.Content | ConvertFrom-Json
    $result = $dataa.result | ConvertTo-Json | ConvertFrom-Json
    $JSON = @{
            type = "A"
            name = "domain.domain.xxx"
            content = $iip
        } | ConvertTo-Json

    if($iip -ne $result.content){
        echo "they are not equal"
        $posturl = "https://api.cloudflare.com/client/v4/zones/"+$zoneId+"/dns_records/"+$result.id
        $test = Invoke-WebRequest -Uri $posturl -Headers $headers -ContentType $contentype -Method Put -Body $JSON
        Write-Host "commit success!"
    }else{ 
        Write-Host "step into sleep"
        
         Start-Sleep -s 600 #这个是暂停时间
    }
}

```

------

**更新：**

> 今天把上面的循环语句删掉了。改成了`windows`系统自带的定时任务功能。真香。

```
$getip = Invoke-WebRequest iiip.co
$iip = $getip.Content.Trim()
$apitoken = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
$zoneId = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
$url ="https://api.cloudflare.com/client/v4/zones/"+$zoneId+"/dns_records?type=A&name=yourdomain&match=all"
$headers = @{"Authorization"="bearer "+$apitoken}
$contentype = "application/json"
$out = Invoke-WebRequest -Uri $url -Headers $headers -ContentType $contentype
$dataa = $out.Content | ConvertFrom-Json
$result = $dataa.result | ConvertTo-Json | ConvertFrom-Json
$JSON = @{
        type = "A"
        name = "yourdomain"
        content = $iip
      } | ConvertTo-Json

if($iip -ne $result.content){
   echo "they are not equal"
   $posturl = "https://api.cloudflare.com/client/v4/zones/"+$zoneId+"/dns_records/"+$result.id
   $test = Invoke-WebRequest -Uri $posturl -Headers $headers -ContentType $contentype -Method Put -Body $JSON
   Write-Host "commit success!"
 }else{ 
   Write-Host "step into sleep"
   Start-Sleep -s 600 #这个是暂停时间
    }

```



<hr/>

##### 更新：

> 2020/01/21 API更新强制加入了ttl

```powershell
$getip = Invoke-WebRequest iiip.co
$iip = $getip.Content.Trim()
$apitoken = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
$zoneId = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
$url ="https://api.cloudflare.com/client/v4/zones/"+$zoneId+"/dns_records?type=A&name=yourdomain&match=all"
$headers = @{"Authorization"="Bearer "+$apitoken}
$tt = $headers | ConvertTo-Json
Write-Host $tt
$contentype = "application/json"
$out = Invoke-WebRequest -Uri $url -Headers $headers -ContentType $contentype
Write-Host $out
$dataa = $out.Content | ConvertFrom-Json
$result = $dataa.result | ConvertTo-Json | ConvertFrom-Json
$JSON = @{
        type = "A"
        name = "yourdomain"
        content = $iip
        ttl = 1
      } | ConvertTo-Json

if($iip -ne $result.content){
   echo "they are not equal"
   $posturl = "https://api.cloudflare.com/client/v4/zones/"+$zoneId+"/dns_records/"+$result.id
   $test = Invoke-WebRequest -Uri $posturl -Body $JSON -ContentType $contentype -Headers $headers -Method PUT
   Write-Host "it's hurt"
 }

```

