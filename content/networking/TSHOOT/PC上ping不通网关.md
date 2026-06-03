---
title: PC上ping不通网关
source: feishu
type: drive
---

PC上ping不通网关
使用==有线网络==通过pc ping不通网关
不适用本故障场景
上网前需要拨号
部署了准入认证的网络，802.1x认证，mac地址认证，web认证
使用DHCP动态获取IP的网络，pc无法获取到ip
客户端采用ipv6地址接入的网络
无线网络
100.64...私网地址
802.1x认证是有客户端，有线的认证
web认证是无客户端，无线WiFi场景下的认证
ICMP报文主要echo报文和echo-reply
可能故障原因
pc终端or操作系统问题
网络中存在ARP欺骗
网络环路
线路link故障
接入交换机配置错误
网关交换机配置错误
处理步骤
在pc上检查本地连接状态
观察网卡指示灯是否保持点亮和闪烁
如果不亮：
（1）在CMD中输入ncpa.cpl，检查网卡是否处于禁用状态。
（2） 将水晶头插紧并适当摇晃。
（3）将另一端水晶头插紧（通常是墻面信息口）。
（4）将网线连接到另一台PC上：
如果该计算机的网口指示灯能常亮，请检查您计算机的设置。
如果该计算机的网口指示灯也不亮，转（5）。
（5）
更换从计算机到信息口之间的网线，观察网卡指示灯是否点如果点亮，则说明之前的网线故障。
如果不亮，则跳转到步骤3，在接入交换机上继续排查。
检查or询问周边pc是否可以正常访问网络
如果周边PC正常，说明是您PC的问题。
如果周边PC也不正常，则说明不是您PC的问题，需要排查网络问题
ping同网段ip
如果能Ping通，则说明接入交换机正常，需要排查网关。
如果不能Ping通，则说明接入交换机不正常，需要排查接入交换机。
pingDNS服务器(8.8.8.8)
若能ping通则网关设置了禁ping，若不能则继续排查
看ARP表
在CMD窗口中输入arp-a命令，检查PC学习到的ARP信息。检查输出中您网关IP地址对应的物理地址（MAC地址）。
如果找不到网关IP地址，则说明PC没有通过ARP解析到网关的MAC地址。
如果找到了网关IP地址，可从MAC地址看出是什么厂商的设备，是否正确。
在CMD窗口中输入arp-d命令，再输入arp-a，检查PC学习到的ARP信息。(每隔几秒反复show)
如果arp-a显示为未找到ARP项，请多次尝试输入arp-a，如果始终看不到网关
IP地址，在网关交换机上继续排查。
如果arp-a 有网关的IP地址，但对应的==物理地址值和之前的不同==，则说明网络中发生了ARP欺骗，需要部署防ARP欺骗功能，具体命令请参照各厂商配置于册
表——无——抓包 表——有——看ip与网关是否一致 攻击：高效+持续
检查防火墙
在运行窗口输入 Firewall.cpl，检查防火墙是否开启，建议直接关闭。
如果可以Ping通，则说明是PC的防火墙阻止了Ping。
如果不能Ping通，可能是交换机配置不正确，继续排查步骤。
网关交换机上检查
记录异常pc的mac和ip，登录到网关交换机上，ping该pc的ip
如果Ping不通，继续下面的排查步骤。
如果能Ping通，检查交换机的接口配置和路由表，分析网络规划是否存在冲突
sh mac-address-table 看MAC表查找pc所在物理接口和三层接口
若没有该pc的mac
该交换机不是故障pc的网关交换机，sh ip int br 看接口状态
交换机到pc路径通信线路有问题，检查接口link
生成树震荡：mac欺骗，mac漂移
看arp表
sh arp dettail查找pc arp信息
没有arp信息 抓包
有arp信息，检查mac address列的值是否与记录的一致，若不一致则说明存在arp欺骗or发生ip地址冲突
age过小，收到攻击or环路
sh int 检查接入交换机上连到网关交换机的链路是否linkup
若line protocol显示为down，若是双绞线，检查水晶头是否插紧，若是光纤，检查光纤收发端是否插反（完全down）
Lastchange time和show version 中的System uptime有差距，sh log检查端口是否多次反复linkup linkdown，若是说明线路有问题，硬件故障
包转发率：每秒能够转发多少数据 1Gbps=1.488Mpps
检查是否发生环路，看速率和计时器
由于show interface counter rate统计速度需要5分钟才能达到测量目材了快速定位，也可以使用show interface counter sumimary命令替代 show int counter rate
先执行clear counter将计数器归零，5秒之后执行show int counter summary；端口的OutBroadcastPkts都是超过6位且头几位基本相同，而OutUcastPkts却小的说明网络发生了环路。
sh ip int br检查三层网关接口状态
检查接口，地址or从地址是否是pc网关，检查掩码是否和pc设置一致，检查status和protocol列是否都是up
若是down说明物理link有问题，检查物理接口
若是administratively down说明网关接口被shutdown
查看物理端口和逻辑接口配置
sh run int +三层逻辑接口，检查是否配置acl是否配置正确
sh run int +二层物理接口，看是否配置QoS/限速，trunk，access是否正确
sh log查找该mac和ip记录信息
sh spanning-tree是否开启生成树
查找该PC所在接入交换机的管理IP地址，登录到接入交换机上继续排查
使用show lldp neighbor 查询该PC所在物理接口的下联交换机的管理IP地址。
如果交换机提示Invalid input detected，则说明该交换机不支持LLDP功能，需要根据网路规划表查阅下联交换机的登录方式。
如果故障PC是直接连接在网关交换机上，没有接入交换机，且以上排查步骤都不能定位故障原因，请保存操作设备的过程日志，联系厂商工程师寻求技术支持
接入交换机上排查
不看arp表，路由表，三层接口状态
通过mac地址表查找该PC连接的物理端口
查看所在端口的配置是否正确
1.如果配置有Ac/Qos/限速，请检查Acl/Qos/限速的配置是否正确。如果您的网络中断，可以尝试将接口上的Acl/Qos/限速no掉，再检查是否能Ping通PC。
2.如果接口的配置中有您不能理解的行，请查阅配置手册。
show log用关联词查找该MAC的记录信息，查找所属物理接口是否有异志。
show spanning-tree，查看是否开启生成树
