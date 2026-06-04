---
title: Pvlan
source: feishu
type: drive
---

Pvlan
私有vlan：局域网内的主机不相互访问
端口类型
Isolated
独立的，不能和其他isolated和community通行
Promiscuous
混合接口，其他两种接口都能从此接口通行
Community
同一个community内可以相互通信
不同的不能通行
命令
vtp transparent (pvlan不支持vtp 要将vtp设置为透明模式)
vlan 10
private-vlan isolated
vlan 20
private-vlan community
vlan 30
private-vlan primary(定义主vlan)
private-vlan association 10,20(定义辅助vlan)
int e0/0
sw m private-vlan promiscuous(定义杂合端口，接路由器设置网关单臂路由)
sw private-vlan mapping 10,20,30(定义杂合接口允许拿下接口通行)
int e0/1
sw m private-vlan host(接口连接主机)
sw private-vlan host-association 30 10
...
