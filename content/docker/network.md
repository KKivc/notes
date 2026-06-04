---
title: network
space: docker
---

# 模式

- bridge：为每一个容器分配、设置ip，并将容器连接到docker0虚拟网桥，默认
- host：容器不会虚拟自己的网卡，配置自己的ip等，而是使用宿主机的ip和端口
- none：容器有独立的network namespace，但没有对其进行任何网络设置
- container：容器不会创建自己的网卡和配置自己的ip，而是和指定容器共享ip、端口范围

## bridge

- 容器和docker0一一对应
- etho——veth

## host

- 不会虚拟出自己的网卡，使用宿主机的ip和端口
- 不需要端口映射，没有意义

## none

- 不会为容器进行网络配置
- 没有网卡、IP、路由等信息，只有一个回环地址
- 需要自己为容器添加网卡、配ip

## 自定义网络

- ip是动态的，通过写死服务名，达到可以ping 服务名
- docker network create xxx
- docker run --network xxx
