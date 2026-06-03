---
title: EtherChanner
source: feishu
type: drive
---

EtherChanner
链路聚合
备份+负载
分类
PAgP
思科私有
f35634e8-88ed-45db-9406-18f44ffe46e0.png


LACP
公有
命令
default int e0/0    //还原接口

---二层---
int range e0/0 -1
channel-group 1 mode desirable(LAgP)/ active(LACP)
int port-channel 1
sw tr en d
sw m dynamic des/tr

---三层---
int range e0/0 -1
no sw
channel-group 1 mode desirable(LAgP)/ active(LACP)
int port-channel 1
ip add 12.12.12.1 255.255.255.0
