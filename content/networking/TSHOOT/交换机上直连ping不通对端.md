---
title: 交换机上直连ping不通对端
source: feishu
type: drive
---

交换机上直连ping不通对端
直连要ping通条件
接口类型要适合
ip，掩码互相落在同一子网
互相arp要正确
754b3e68-df5e-44e3-b120-23dff408224f.jpeg

二层接口
trunk，access，portchannel，pvaln
三层接口
portchannel，svi，loopback，no switchport，路由接口
配置类问题
环境类问题
攻击
环路
线路问题
软硬件bug
交换机
盒式交换机
多用于接入层，尺寸单位 u，1u=4.445cm
55afc834-1e34-4163-9bfa-1bfc5189731d.png

箱式交换机
多用于核心层
ca09ced4-720f-4783-96ea-96341721fb72.png

主控板：相当于电脑cpu
3ebcd1ef-6ca1-47f7-a741-4688e9e1cf2d.png

线卡：相当于一个个盒式交换机
故障现象
本端采用trunk access no sw形式，ping不通对端交换机
交换机上vlan mac只有1：对端交换机开了no sw，应该是tr
交换机上vlan只有1 mac有多个：对端交换机开了access
故障处理
看arp，mac表
相互之间的arp表对应关系要正确
检查接口
sh int 检查连接对端的接口是否有linkup
检查交换机配置
158bebd8-8729-4535-a7e2-a2fdc4e4c1a1.png


2910076b-5ecc-4823-bfc3-959c0b8452b1.png

A/B：1.是否有tag 2.是否接收 3.送进哪个svi/三层口
native不能打tag，access接收所有不带tag的流量，no sw属于三层不接收二层tag
检查双方ip，掩码配置是否正确
检查接口是否配置了acl/qos/限速
检查接口编号是否配置错误
判断接口是否接错：拔对端看本端
检查交换机硬件工作状态
检查堆叠(stack)or vss虚拟化(两个大的交换机虚拟化成一台)成员状态是否就绪
sh member 查看堆叠成员状态，sh sw virtual role看vss成员状态
检查模块化交换机线卡是否正常工作
检查交换机软件版本
检查CPU状态
1.如果cpu利用率超过50%，请首先排查此问题，跳转到CPU利用率高问题处理的章节。
2.如果没有超过50%，检查机箱式交换机的线卡CPU利用率（各厂商命令不同）、如果cpu利用率超过50%，请首先排查此问题
尝试更换物理和三层逻辑接口(svi)
