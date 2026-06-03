---
title: BGP邻居无法建立
source: feishu
type: drive
---

BGP邻居无法建立
故障现象
R1和R2之间BGP邻居关系无法建立
邻居建立的两个条件
能够建立tcp会话
能够正确的交换open报文
建立tcp会话时需要关注两点
IP层的连接有效（有从IGP得到的路由，or配置了静态路由）
端口179能够使用
正确交换open报文需要关注两点
open报文正常收发
open报文参数匹配
邻居不能建立
检查as号是否正确
检查对等体IP地址是否正确
检查本端与对等体的RID是否一致
如果使用环回接口，检查是否配置了update-source loopback。缺省情况下，路由器使用最佳路由建立tcp连接，而不是loopback接口
使用扩展的ping命令检查TCP连接是否正常，由于一台路由器可能有多个接口能够到达对端，应使扩展的ping命令指定发送ping包的源IP地址。如果Ping不通，使用show ip route命令检查路由表中是否存在到邻居的可用路由。如果ping通，检查是否配置了禁止tcp端口179的acl
若是ebgp邻居，且ebgp连接在物理上不是直连，检查是否配置 nei ebgp-multihop
holdtime定时器不一致，选较小的
能力参数字段不一致
