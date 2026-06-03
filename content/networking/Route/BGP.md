---
title: BGP
source: feishu
type: drive
---

BGP

Date: 2024-08-16
路径矢量
依赖与TCP协议
范围大小：ospf<isis<bgp.
AS区域自治系统(area)
公有1-65535
私有64512-65535
每经过一个AS都会被记录
BGP中下一跳是下一个AS号入口地址
特性
具有可靠性更新：使用==TCP179==号端口传输<TCP进行三次握手>
增量触发性更新
阶段性发送keepalive(hello包)消息维持关系
丰富的metric，默认20
应用与大型网络
分类
EBGP
条件
不同的AS号
定义出邻居
TCP握手成功
命令
router bgp 1<as号>
neighbor 10.1.1.2<需要形成邻居的ip> remote-as 2<邻居所在的as号>
router bgp 1
network 1.1.1.0 mask 255.255.255.0<正掩码>     //将路由表中的接口上传到bgp表中  ip形式与路由表中一样
ip route 2.2.2.0 255.255.255.0 null 0<垃圾桶   若没有目的接口>
network 2.2.2.0 mask 255.255.255.0      //若路由表中没有此接口想上传bgp则设置一个静态路由使流量进入null 0使得路由表中有2.0的网段
neighbor 2.2.2.2<环回地址> ebgp-multihop <若有目的接口要补充   状态为idle>   //是环回接口且ebgp就要写
EBGP传递规则：同步<默认关闭,关闭就可以传递>
BGP与IGP里面要同时存在条目，IBGP才能将条目传递给EBGP
使用重分布<意味着IBGP区域内的路由器的路由表都有该条目(IGP)>
IBGP
条件
相同的AS号
定义出邻居
TCP握手成功
命令

---先在区域内部配动态/静态使TCP协议联通---

router bgp 1<as号>
neighbor 10.1.1.2<需要形成邻居的ip> remote-as 1<邻居所在的as号>

---若不使用物理接口使用环回接口    先前bgp通的物理接口先no掉，**环回IP要先上传路由表**---
router bgp 1<as号>
neighbor 2.2.2.2<需要形成邻居的环回接口ip> remote-as 1<邻居所在的as号>
neighbor 2.2.2.2 update-source loopback 0<自己的>     //有环回接口就要写

---改换下一跳地址  谁是下一跳在谁上面改---
Router bgp 1
neighbor 4.4.4.4<邻居ip> next-hop-self   <告诉4.4下一跳是它>   //没写下一条是下一个as
IBGP条目传递规则：从IBGP邻居接收的条目，不能传给其他的IBGP邻居
路由映射器：使IBGP邻居接收到<中介，将其他邻居作为客户端> or 做全互联
BGP形成邻居条件并不要求直连只要TCP可通可以间隔形成邻居
BGP聚合路由
认证（MD5）
命令
- nei 1.1.1.1 password mykey
clear ip bgp * ：重启bgp邻居<重新连接> //or 把 *去掉换成特定邻居ip
clear ip bgp 1.1.1.1/ * soft in/out:刷新参数
BGP路径属性
BGP选路规则
权重
优先级
next hop = 0.0.0.0
as path
条目的来源方式：IGP<EGP<inconplete（重分布）
MED
EBGP优先于IBGP
weigh attribute（权重）（in）
越大越优先
只在本设备有意义
思科独有
local preference (优先级)（in）
只能在本AS内传递
接收后才能修改
默认100
越大越优先
AS path
数量少的优先
MED(metric)（out）
同一个as传来的med才能比较
只能传一跳
默认0
上个设备修改后放出来
access-list ...<bgp表中network中的网段>
route-map list1 permit 10
match ip add ...
set local-preference 150<设置优先级>
set weight 200<权重>
router bgp 1
nei 10.0.0.1 route-map list1 in/out

route-map list1 permit 20 
