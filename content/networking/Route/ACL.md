---
title: ACL
source: feishu
type: drive
---

ACL

Date: 2024-08-17T17:45:00
功能
过滤
匹配感兴趣流量
给数据流分类
定义3IP层 4协议层数据流
使用场景
过滤access-group
NAT
VTY控制access-class
分类
标准ACL
只匹配源地址<只知道从哪里来，不知道去哪里，不能匹配协议>
序号范围：==1-99==，1300-1999
命令
- access-list 1 permit 10.10.10.1 0.0.0.0(= host 10.10.10.1)
- access-list 1 permit any

---定义接口---
int f0/0
ip access-group 1 in/out
扩展ACL
匹配源地址，目标地址，协议
序号范围：==100-199==，2000-2699
命令
---协议 源IP 目标IP
- access-list 100 permit tcp 10.10.10.0 0.0.0.255 23.23.23.0 0.0.0.255 eq23
- access-list 100 permit ip any any


---定义接口---
int f0/0
ip access-group 100 in/out
命名ACL
命令 //添加ACL条目只能在命名ACL使用
---命名标准ACL---
- ip access-list standard list1<名字>
- (15顺序)permit 172.16.1.0 0.0.0.255

---定义接口---
- int f0/0
- ip access-group list1 in/out

---命名扩展ACL---
ip access-list extended list1
permit ip 172.16.1.0 0.0.0.255 any

---定义接口---
int f0/0
ip access-group list1 in/out
特点
默认拒绝
删一全删
从上到下
自身产生的流量，无法过滤
