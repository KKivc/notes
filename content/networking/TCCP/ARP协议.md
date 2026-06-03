---
title: ARP协议
source: feishu
type: drive
---

ARP协议
地址解析协议
arp协议工作在网络层和数据链路层之间，通常被认为是一个跨两层的协议。
IP数据报文必须封装成帧才能通过数据链路进行发送。数据帧必须要包含目的MAC地址，因此发送端还必须获取到目的MAC地址。通过目的IP地址来获取目的MAC地址的过程是由ARP协议来实现的。

作用
把IP地址解析成mac地址
数据在以太链路上以以太网帧的形式传输
要在以太网中传输IP数据包，必须知道IP对应的mac
对于目标IP：手动获取：ping；   自动：DNS
源IP：手动:手动填写 ；  自动：DHCP
源mac：自动：厂商分配
目标mac：自动：arp  
同一网段arp地址解析
同一网段内的目的mac为目的主机的mac
先判断是否同一网段：2次与 1次异或
查看arp表，若arp表中没有目标主机对应的表项，则生成目标mac是全F的广播地址的arp请求，本地生成临时条目
进行自学习（将对方的IP，mac填充到arp表），arp单播应答
覆盖临时条目
根据arp表将目的mac封装完成
ac23e663f71441bb63ce7cb05f5fc807_720.jpg

不同网段arp地址解析
不同网段内的目的mac是网关的mac
同上

一次路由多次交换
源目IP不变
源目mac逐跳变
arp：辅助路由打通每一跳
mac地址表三要素：mac地址，出接口，vlan
arp缓存
动态表项：通过arp协议学习，能被学习，缺省老化时间120s
静态表项：手动
自发arp
作用：检测IP地址是否发生冲突
在没有人问自己的情况下，无缘无故自问自答
更新arp表项
触发：局域网IP地址冲突时，地址修改或变更时，DHCP分发地址时，ARP缓存表清理时，网关冗余协议HSRP交互时，TFTP协议传输数据前，开机or更改IP地址，会发送自发arp
代理arp
别人的IP回应自己的mac（R2）
常用于跨网段访问



防arp欺骗  
Arp request报文更新arp表的条件：arp报文中target IP为自己，用arp报文中sender IP和sender mac更新自己的arp表
Arp reply报文：已存在sender IP表项
自发arp：当前已存在
判断：主机设备：网络时断时续or网速慢；在命令行执行arp-d，在执行arp-a看网关对应的mac地址发生改变
网关设备：arp表中同一个mac对应多个IP

安全地址
定义：主机的真实信息，IP+mac
获取：手工指定：port-security，自动：DHCP snooping、dot1x认证
