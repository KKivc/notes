---
title: EIGRP
source: feishu
type: drive
---

EIGRP

Date: 2024-08-19T17:00:00
算法--DUAL算法
当链路断后，没有了最优和备份条目后，切换成SIA（active）状态，该路由器会向其他路由器以组播形式发送query报文，有响应的路由器将以单播形式发送reply报文
88号协议报文
特点
AD值90
组播，单播代替广播
支持多种网络层协议
快速收敛
部分更新<有变化的更新，节省路由流量>
负载均衡
邻居的形成
7187dd04-2d4f-4863-b940-dfd781e08f97.png

命令
- router eigrp 1<要一样>
- network 1.1.1.1 0.0.0.0
metric
带宽加延时
接口两端带宽要一样
passive interfaces
启用后hello包发不出去 邻居断掉
命令
router eigrp 1
passive-interface e0/0
EIGRP Tables
FD（Feasible Distance）由本地路由器去往目标的metric值 要加上本身的
AD（Advertised Distance）由邻居去往目标的metric
Successor 最优路由器 最低的FD 将进入路由表
Feasible Successor 备份路由器 （AD<最低FD）进入拓扑表
