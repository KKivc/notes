---
title: DHCP
source: feishu
type: drive
---

DHCP
动态主机配置协议
UDP报文
由服务器对客户机动态分配TCP/IP信息
IP地址
子网掩码
默认网关
首选DNS服务器（域名解析：把域名对应的IP地址进行解析）
优势
减小工作量
减小输入错误的可能
避免IP冲突
当网络更改IP地址段时，不需要重新配置每台计算机IP
DHCP分配过程
DHCP Discover报文：client->server广播
DHCP Offer报文：server->client广播(client还没有IP)server收到discover报文后给client==分配IP及其他信息==
DHCP Request报文：client->server，client收到offer报文后选择第一个的回应offer的server，并以广播形式发送DHCP Request报文，隐式拒绝其他server
DHCP ACK报文：server->client，被选择的服务器以广播形式给客户机发送DHCP ACK报文，通知client可以正式使用分配的IP地址
DHCP NAK报文：server->client，通知client无法分配使用合适IP地址，以单播形式（公司违约）
DHCP Release报文：单播，client->server告知server不再需要分配IP，让server释放被绑定的IP租约(个人辞职)
DHCP Decline报文：client->server，通知server所分配的IP地址不可用，client收到server回应的ACK报文，通过冲突检测机制发现server分配的地址冲突or其他原因不能使用，在正式使用分配的IP地址时都要冲突检测机制，单播（个人违约）
DHCP Inform报文：client->server请求获取更详细的配置信息，单播
六个阶段
发现阶段
提供阶段：服务器提供IP地址
选择阶段：收到多个offer，选第一个收到的
确认阶段
重新登陆：以后client重新登陆网络时，不再需要发送discover，而是直接发送包含前一次所分配的IP地址的request请求信息，若行server发送ACK，不行server发送NAK，client又重新从discover开始
更新租约：client启动时和IP租约期限过一半时，会自动向服务器发送更新IP租约的信息（request）
命令
57fdbad3-9a3e-48ce-9109-c25676257be3.png


一个地址池一个网段，pc要no sh， 手动在pc指定网关命令ip default-gateway
pc跨网段要设置中继路由，pc以广播发送到中继转化为单播发送给服务器
27805b74-c1a5-489d-a5d3-83941583c70f.png

三种分配IP地址机制
手动：为特定的某台pc配置特定的地址
自动：允许DHCP服务器为第一次上网的pc分配一个永久地址
动态：服务器可以使pc在一段时间内租用一个地址
server分配地址优先顺序
手动
client以前的地址（重新登陆/更新租约）
option82
从地址池中分配一个可用地址
租约到期和冲突地址
DOS攻击
拒绝服务式攻击
黑客客户端不断生成新的mac地址发送request报文请求，使得服务器pool池IP占满，当合法的客户端想进入就进不去
DDOS攻击
分布式DOS攻击
DHCP Snooping
将与主机相连的接口设置为Untrusted，Untrusted接口不能转发DHCP响应报文
命令

ip dhcp snooping
ip dhcp snooping vlan 10
int f0/0
ip dhcp limit rate 50    //限制流量，只能处理50个
int f0/1
ip dhcp snooping trust    //开启snooping后交换机上所有接口默认untrust，除了与主机相连的接口untrust外其他要trust


---思科服务器默认不信任中继代理，分配不了ip---
int valn 10
ip dhcp relay information trusted     //在server上操作，忽略掉中继代理
