---
title: OSPF 
source: feishu
type: drive
---

OSPF 

Date: 2024-08-15
协议号89
组播地址：224.0.0.5
SPF算法---最短路径优先
特性
独立传输
采用高效的更新
更新目的地址
组成
ABR区域边界路由器：连接两个不同区域的路由器、
ABSR自治系统边界路由器：与外部路由协议连接的路由器
域内路由器：除area0外的路由器
核心路由器：area0内的路由器
通信
Hello包内形成邻居的条件
计时器一样
area ID一样
认证密码，类型一样
邻居——>邻接
1d42619a-929a-4f24-bb6d-0bf0430fe958.png

- router ospf [prosess-id <可不一样>]
- network 网段 反掩码 area[area-id]       //配置命令
网络发生变化发送LSU报文： DR<指定路由器 班长> 与 BDR<备份的 副班长> 有且只有一个 要与所有的DRother<成员>形成邻接关系形成数据库同步 DRother形成TWO-way状态<邻居> 发送给DR BDR的更新报文使用==224.0.0.6==
LSA
相当于LSU报文
分类
一号LSA---Router LSA
域内传递，不会穿过ABR
包含链路类型，直连链路列表，网段前缀
由本身路由器产生通告 <显示的RID是通告路由器上的>
二号LSA---Network LSA
域内传递，不会穿过ABR
包含直连链路信息，网段前缀
由DR产生
三号LSA---Summary LSA
在整个ospf区域内传递，从area1到area2
包含网段信息<将一号与二号信息进行整合>
由上游ABR产生，每经过一个ABR，通告路由器都发生改变
四号LSA---ASBR Summary LSA
在整个ospf区域内传递，从area1到area2
包含ASBR的RID
由ABR产生
五号LSA--- External LSA
从外部路由协议进入ospf区域的传递
包含网段信息
由ASBR产生
四号与五号共同工作 协同作用
虚链路
建立一条链路形成一个区域，将两个不连续的区域连接
- area 1<链路所在区域> virtual-link 2.2.2.2<对面rid>   //两端相互配


---虚链路中有一端开了认证则另一端必须开认证---
- area 1<链路所在区域> virtual-link 2.2.2.2<对面rid> authentication-key mykey
- 
Cost(metric)
计算分类
E1：每条metric都会相加 更真实反应链路 E2：进去后metric不变
公式：100M<10^8 B> / 带宽 <100M为参考带宽，一般需要修改，一旦修改所有设备都要改>
- auto-cost reference-bandwidth 10000     //参考带宽修改
汇总[[汇总 ]]
减少LSA的泛洪，减少路由条目，减少CPU资源
三号LSA区域间的汇总，在ABR上操作
- area 1 range 172.16.8.0 255.255.248.0
五号LSA外部协议进入ospf的汇总，在ASBR操作
- summary-address 172.16.8.0 255.255.248.0
默认路由
进行外网进出
五号LSA在==ASBR==操作，不加always则设备本身由默认路由，若加则自动生成
- default-information originate (always)
认证
两端做认证的密码要一样
认证成功：邻居形成
明文认证
命令
---在接口起---
- int ...
- ip ospf authentication 
- ip ospf authentication-key mykey<密码>

---在进程起---
- int ...
- ip ospf authentication-key mykey
- router ospf 1
- area 0 authentication
暗文认证
命令
---在接口---
- int ...
- ip ospf authentication message-digest


---在进程---
- router ospf 1
- area 0 authentication message-digest

---最后都要在接口配密码---
- int ...
- ip ospf message-digest-key 1 md5 mykey
