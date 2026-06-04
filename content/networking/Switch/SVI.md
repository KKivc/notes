---
title: SVI
source: feishu
type: drive
---

SVI
交换机虚拟接口
不同vlan之间可以通信
命令
5ba03df7-5b16-4aa9-82f9-41f8e8f8e4b3.png

---二层交换机开启路由功能---
vlan 10， 20    //vlan要存在
ip routing 
int vlan 10
ip add 10.10.10.254 255.255.255.0    //相当于vlan 10的网关
no sh
int vlan 20
ip add 20.20.20.254 255.255.255.0
no sh


-----------
---交换机变为三层接口---
ip routing
int f0/0
no sw 
ip add 10.10.10.3 255.255.255.0
