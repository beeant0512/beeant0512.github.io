title: Mac下双网卡设置路由区分无线和有线
author: Beeant
tags: 
  - wifi
categories:
  - Mac
date: 2016-06-21 08:57:00
---
背景：用无线访问外网，用有线访问内网。由于有些ip只能通过内网访问，因此需要手动设置路由，实现指定ip(段）走有线。  
  
MAC route指令：  

### 查看当前路由表
```
netstat -nr
```
### 添加路由
```
sudo route add -net 0.0.0.0 192.168.1.1 默认使用192.168.1.1网关
sudo route add 10.64.20.0/24 10.17.12.254 内网地址使用内网网关
```