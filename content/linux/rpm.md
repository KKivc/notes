---
title: rpm
source: feishu
space: Linux
---

rpm
查询
已安装的rpm包
rpm -qa | grep xxx
rpm -q xxx
rpm -qi xxx：含有详细信息
rpm -qf 文件全路径名：查询文件所属的软件包
卸载
rpm -e rpm包的名称
--nodeps 强制
安装
rpm -ivh rpm包全路径名称
-i：install
-v：提示
-h：进度条
 --nodeps强制
yum
能够从指定服务器下载rpm包并安装，自动处理依赖关系，不用下载rpm包到本地
yum list | grep xxx：查询yun服务器是否有需要安装的软件
yum install xxx：下载安装

