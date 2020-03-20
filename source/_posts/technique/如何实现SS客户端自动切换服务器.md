---
title: 如何实现SS客户端自动切换服务器
date: 2019-11-15 10:10:39
tags: 技术
keywords:
description:
---

如何实现 `Shadowsocks` 客户端自动切换服务器呢？这里的自动切换仅仅是切换，没有附加条件的切换。根据其配置文件可以找到入手点。



<!--more-->



其配置文件内决定当前活动服务器的是一个`index`参数。这个参数就是所有配置信息在配置文件中的顺序，所以，想办法自动改变这个参数就可以实现自动切换的目的。

**计划**

- [x] Windows 下使用 Powershell 来解决
- [ ] Windows 下使用 Python 来解决

完成后相应的代码会贴在下面

<hr>

##### PowerShell 版

```powershell

#获取json文件
while(1){
    $pattern = "\d{1,3}.{1,3}\d.{1,3}\d{1,3}"
    $t=(Get-Random -Minimum 500 -Maximum 600)
    $json = (Get-Content -Raw -Path "X:\XXX\XXX\XXX\gui-config.json" | ConvertFrom-Json)
    Write-Host "Start! Refresh in $t seconds..." ( Get-Date)
    Write-Host "当前活动服务器: " $json.configs.Get($json.index).server "序号："$json.configs.length"-"$json.index
    Start-Sleep -Seconds $t
    $json.index+=1
    $i = $json.index
    #判断当前index 是否在正确范围内，如果在则进行下面的操作，目前存在的问题是不知道第3个服务器状态是否可用
    if($i -gt 1 -and $i -lt $json.configs.length) {
          if(!(Test-Connection $json.configs.Get($json.index).server -Quiet)){
        do{
            $json.index+=1

        }while(Test-Connection $json.configs.Get($json.index).server -Quiet)
    } 
    }else{

        $json.index = 2
    }
    ($json | ConvertTo-Json | Out-File -FilePath "X:\XXX\XXX\XXX\gui-config.json")
    Write-Host "停止 XXX"
    Stop-Process -Name Shadowsocks
    Write-Host "停止 XXX"
    
    $target = $json.configs.Get($json.index).server
    if($target -match $pattern){
        $ip=$target
    }else{
         $ip=([System.Net.Dns]::GetHostAddresses($target) | ConvertTo-Json | ConvertFrom-Json).IPAddressToString
    }
    $r= (Invoke-WebRequest http://ip.taobao.com/service/getIpInfo.php?ip=$ip).content | ConvertFrom-Json
    Write-Host $r.data.country $r.data.region
    Write-Host "启动 XXX"
    Start-Process -FilePath "X:\XXX\XXX\XXX\Shadowsocks.exe"
 
}
```

<hr/>
更改了检测方式，每次循环都先把 index+1 之再进行可用性判断。

```powershell

#Get json File
while(1){
    $pattern = "\d{1,3}.{1,3}\d.{1,3}\d{1,3}"
    $t=(Get-Random -Minimum 120 -Maximum 300)
    $json = (Get-Content -Raw -Path "X:\XXX\XXX\XXX\\gui-config.json" | ConvertFrom-Json)
    Stop-Process -Name Shadowsocks
    $json.index+=1
    $i = $json.index
    if($i -gt 0 -and $i -lt $json.configs.length) {
        ($json | ConvertTo-Json -Compress | Out-File -Encoding utf8 -FilePath "X:\XXX\XXX\XXX\gui-config.json")
        Start-Process -FilePath "X:\XXX\XXX\XXX\Shadowsocks.exe"
        do{
            $json.index+=1
            Stop-Process -Name Shadowsocks
            ($json | ConvertTo-Json -Compress | Out-File -Encoding utf8 -FilePath "X:\XXX\XXX\XXX\gui-config.json")
            Start-Process -FilePath "X:\XXX\XXX\XXX\\Shadowsocks.exe"
            try{
            $statusCode = (Invoke-WebRequest -Uri "http://www.t66y.com" -Proxy "http://127.0.0.1:1080" -TimeoutSec 5).statusCode}
            catch{
            $statusCode = 500            
         }
        }while($statusCode -ne 200)
    
    }else{
        $json.index = 0
    }
       <#检测主逻辑，简单判断IP地址是否可以ping通，但是不对 SS 能否正常连接做检测所以，以下方法不好用。    
    
              if(!(Test-Connection $json.configs.Get($json.index).server -Quiet)){
            do{
                $json.index+=1
            }while(Test-Connection $json.configs.Get($json.index).server -Quiet)
        } 
        }else{
            $json.index = 0
        }
       #>  

    ($json | ConvertTo-Json -Compress | Out-File -Encoding utf8 -FilePath "X:\XXX\XXX\XXX\gui-config.json")
  
    $target = $json.configs.Get($json.index).server
    #IP地址检测
    if($target -match $pattern){
        $ip=$target
    }else{
         $ip=([System.Net.Dns]::GetHostAddresses($target) | ConvertTo-Json | ConvertFrom-Json).IPAddressToString
    }
    $r= (Invoke-WebRequest http://ip.taobao.com/service/getIpInfo.php?ip=$ip).content | ConvertFrom-Json
    Write-Host "==>Current Location ==>"$r.data.country  $r.data.region

    Write-Host "==>开始! Refresh in $t seconds..." ( Get-Date)
    Write-Host "==>Current Server: " $json.configs.Get($json.index).server "Index: "$json.configs.length"-"$json.index
    Start-Sleep -Seconds $t
}
```







<hr>

##### 更新：

​	11/16  加入IP地址属地查询并印到控制台。

​	11/17 加入 SS 连通性检测，保证每一次连接都有效。