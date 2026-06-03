---
title: RSTP
source: feishu
type: drive
---

RSTP
快速生成树
802.1W
新增端口角色
NDP：A与B
替代接口（Alternate）：接收其他网桥发送来的BPDU
备份接口（Backup）：用于学习自己发送的BPDU
改进端口状态
90dff968-4f03-4ab7-964c-1c9b84fac421.png

只有配置BPDU
无论非根桥是否收到根桥传来的配置BPDU，非根桥仍然按照Hello Time时间间隔发送BPDU，而STP需要由根桥触发
6s更短的BPDU超时时间
当端口收到上游的BPDU会与自身缓存的BPDU进行对比，若自身的优于收到的，那么该端口会直接丢弃收到的BPDU，立即回应自身缓存的BPDU，加快收敛速度
快速收敛机制
根端口快速切换：网络中一个根端口失效，则网络中最优的A口将成为根端口，进入Forwarding状态
指定接口快速切换：网络中一指定接口失效，则网络中最优的B口将成为指定端口接入Forwarding状态
边缘端口：接主机的接口，不参与RSTP计算，可以由Discarding直接接入Forwarding，一旦边缘端口接交换机收到BPDU就成为了普通的STP端口，引起网络震荡
