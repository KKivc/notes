---
title: OSPF协议邻居关系不能建立
source: feishu
type: drive
---

OSPF协议邻居关系不能建立
确认邻居是否建立
沿途路由表，源ip 目的ip正确
trace route定位
故障现象
R1和R2之间的OSPF邻居(tow-way)关系无法full(邻接)
影响邻居建立本质
数据包的收发
数据包参数
处理步骤
版本号是否一致——参数
检查配置，确认ospf network语句是否将接口宣告——收发 sh ip os int br(检查接口是否开启ospf协议)
检查到邻居接口是否up，ping对端地址是否能通——收发
检查是否有acl阻断ospf报文，ospf使用==IP协议==，协议号89——收发
检查到达ospf邻居的接口是否被passive(一般设置在网关上 svi口，要让内网知道又不起ospf邻居)，被passive的接口，建立和维护ospf邻居状态的hello报文不会发送，邻居关系将不能full——收发
检查两边定时器是否一样——参数
ospf接口的网络类型要一样 有DR/BDR的网络类型：MA多路访问(一台设备出来都能访问其他三台设备)——收发/参数
11b57121-76ed-4593-bcc4-93de98144ca4.png

检查ospf接口子网掩码是否一致——收发/参数 debug ip ospf hello
检查ospf接口所在区域是否一致——参数
检查ospf两端的认证类型是否匹配——参数
若ospf有特殊区域存在，如stub或nssa区域，则要检查两端区域的区域类型是否一致——参数
检查接口两端mtu是否一致，若不一致，则ospf邻居可能卡在exchange or exstart状态不能full——参数
