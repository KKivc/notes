---
title: HSRP
source: feishu
type: drive
---

HSRP
思科私有
多台设备虚拟出一台路由器作为pc的网关
命令
---sw1---
int vlan 10
ip add 10.10.10.1 255.255.255.0    //先设置SVI
no sh
standby 10 ip 10.10.10.254     //两台要一样
standby 10 priority 110     //设置优先级，默认100，若一样则比较IP，谁大谁优先
standby 10 preempt       //参与竞选

---sw2---
int vlan 10
ip add 10.10.10.2 255.255.255.0    //先设置SVI
no sh
standby 10 ip 10.10.10.254      //两台要一样
standby 10 preempt       //参与竞选


sh standby br
a55e31cc-dd01-4af4-8bff-2e0d7fa73451.png


pc发送ARP，active router进行解析，优先级高的成为active router
HSRP与STP
根桥一般为active router
IP SLA
检查链路的可达性

ip sla 1
icmp-echo 10.10.10.1    //对方ip
frequency 5   //5s发送一次报文
ip sla schedule 1 now life forever   //立即生效

sh ip sla sum
Multiple HSRP Group
负载均衡

---sw1---
spanning-tree vlan 10 root primary
spanning-tree vlan 20 root secondary      //使vlan 10的流量都往sw1上跑

---sw2---
spanning-tree vlan 20 root primary
spanning-tree vlan 10 root secondary      //使vlan 20的流量都往sw2上跑
