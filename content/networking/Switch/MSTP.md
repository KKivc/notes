---
title: MSTP
source: feishu
type: drive
---

MSTP
802.1S
多个vlan共用一个生成树
MSTP将多个vlan映射到一个instance（实例）相当于vlan的集合，映射到同一个instance的vlan共享同一棵生成树
MSTP Region
每个域内形成多个生成树实例
MSTI(instance)
每个生成树都称为一个MSTI，不同的MSTI包含不同的vlan
CST
公共生成树，是连接交换网络内所有MTP域的一棵生成树
6cc539d4-f3bc-4da9-b5bf-0fdbfe65ae3c.png

IST
内部生成树，各MST域内的一棵生成树，MSTI的instance id为0
CIST
公共和内部生成树，连接一个交换网络内所有交换设备的单生成树
命令
spanning-tree mode mst
spanning-tree mst conf
name ccc(域名)   //用于区分域
revision 1（默认0）   //用于区分域
instance 1 vlan 1，3
instance 2 vlan 2，4
spanning-tree mst 1 root primary
spanning-tree mst 2 root secondary
