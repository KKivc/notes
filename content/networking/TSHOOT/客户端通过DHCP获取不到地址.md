---
title: 客户端通过DHCP获取不到地址
source: feishu
type: drive
---

客户端通过DHCP获取不到地址
接入网络长时间观察，电脑网卡本地连接是受限制或无连接
故障处理步骤
排查客户端及操作系统问题
查看客户端是否为动态获取IP
通过pc安装抓包
排查网络环境问题
确定客户端与服务器之间物理连接连通正常：尝试将pc设置为静态IP及网关，ping服务器IP，若能ping通且延迟<10ms，没有丢包或抖动说明连接畅通，进入下一步排查
查看设备是否存在正确路由，将路由调整正确（ping不通）
排查是否有环路和攻击现象（能ping通但延迟大有丢包）
查看沿途交换机cpu占用是否过高，逐点show交换机cpu
排查中间设备或链路上的加密机，ACL，端口安全是否过滤掉了bootps(UDP 68),bootpc(UDP 67)
查看是否有其他功能影响：ACL，PVLAN应用，Super Vlan应用，MSTP的block端口
排查网络设备配置是否正确
同一台设备中继和server不能同时配，SNP和server能同时配
sh run查看设备配置信息
relay一般配置在三层网关设备上
排查DHCP server性能问题
检查是否超出DHCP server的容量和性能
地址池内是否有可用IP
增加地址池
