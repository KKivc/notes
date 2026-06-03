---
title: IPSec
source: feishu
type: drive
---

IPSec
产生背景
用户在互联网上传输数据容易被窃取（dos攻击）/篡改/身份欺骗，需要安全手段保证通信机密性、完整性(哈希算法HASH，雪崩效应、单向性、冲突避免)、合法性(源认证，key<Presharekey  预先配好的两个一样key   HASH+key=HMAC>、数字证书)、不可否认性(数字签名)
IPSec协议(一组协议)概述
使用下面两种协议对IP报文进行保护
AH协议(协议号51)
明文
AH与NAT不兼容
AH的验证范围比ESP大
image.png

ESP协议(协议号50)
密文，多了加密算法
image.png

 IPSec协议使用AH或ESP对报文保护，存在两种保护模式
传输模式
仅对IP头部以上数据部分实施保护
+AH
image.png

+ESP
发送方先加密后认证，接收方先认证后解密
fef9757aa0c584e5a70c5f5b4fb9f94f_720.jpg

e6aaafd7e70013308e3c71ef27a56fad_720.jpg

隧道模式
对包括IP头部在内的数据部分实施保护
+AH
9b907d7d2e763cac105a522f5e36a151_720.jpg

+ESP
6b2230f3438a80d4fa00e8fcbc3f14dd_720.jpg

bf0e41c57e66ead2bfbe90e2fdae5883_720.jpg

SA
安全关联，两个IPSec实体之间的协商，是构成IPSec的基础
SA是单向的，入方向负责接收到的数据包，出方向负责处理要发生的数据包，因此每个通信要有两种SA，这两个SA构成一个SA束
SPI：安全参数索引，用与标识具有相同IP地址和相同安全协议的不同SA。SA是单向的，因此本地的出方向SA的SPI一段与对端的入方向SA的SPI相同
IP的目的地址：IP目的地址，它是SA的终端地址
序列号：用于产生AH或ESP头的序号字段，仅用于外出数据包。SA刚建立时，该字段为0，每次保护完一个数据包，九八序列号加1
SADB
image.png

SP
image.png

image.png

如何产生SA
IKE自动管理
Internet密钥交换(Internet Key Exchange)，用于动态建立SA
SKEME
提供为认证目的使用公开密钥加密机制
Oakley
提供两个IPSec对等体间达到相同加密密钥的基本模式的机制
ISAKMP
定义了信息交换的体系结构，包括两个IPSec对等体间分组形式和状态转变
ISAKMP报文可以利用UDP或TCP，端口号都是500，一般用UDP。IKE使用ISAKMP消息来协商并建立SA
两个IPSec实体之间的IKE协商分为两个阶段
第一阶段：建立ISAKMP SA(IKE SA) 
两种模式
主模式：6条ISAKMP消息交互
第一、二个ISAKMP报文：用于交换并协商保护ISAKMP消息的安全参数及对等体验证方式
第三、四个ISAKMP报文：用于交互IKE的密钥交换和随机值载荷，交互信息用于使用DH算法计算出共同的密钥材料，结合随机值载荷及cookie值，并使用随机数算法PRF得出4个密钥
image.png

DH算法：公钥分发系统，使用非对称密钥加密机制 （1.公钥加密、私钥解密 2.私钥加密、公钥解密<数字签名>，特点：慢、稀松，保护材料、key<小>   对称密钥加密特点：快、紧凑，保护数据<大>） 
第5、6个ISAKMP报文：用于交换身份载荷和HASH载荷。第5、6个报文是经过保护的
image.png

总结
image.png

积极模式：3条ISAKMP消息交互
IKE SA是为第二阶段的ISAKMP消息提供安全保护
第二阶段：建立IPSec SA
快速模式：三条ISAKMP消息交互 
第一个报文：
image.png

第二个报文：
image.png

第三个报文：
image.png

IPSec SA是为IP诗句提供安全保护
ISAKMP报文格式
f5ced33076a9a25061d3f27e3098da15_720.jpg

ed3ae87472900b1240b57234ba235f09_720.jpg

报文id：32bit
在IKE第一阶段该值全0
第二阶段有发起方生成随机值，唯一报文标识可以唯一确定第二阶段的协议状态
ISAKMP报文携带的载荷
双方交换的内容称为载荷。对于一个用基于ISAKMP密钥管理协议交换的消息来说，其构建方法：将ISAKMP所有载荷链接到ISAKMP报头
image.png

3aac3566544f09daaae6d7fc0226212d_720.jpg

IPsec配置步骤
Crypto map：做关联，只能配置在出接口
db35e98a7696979b1a434972271938d3.jpg

915f410d684e0b49338b0e75aef72cb0_720.jpg

0870928ead77320c95ca5f828d010f7c_720.jpg

468a3af8319a05bba94ac8c2e23a13e6_720.jpg

9b88bd1d918b91af922be3606a5397fd_720.jpg

dba75ae9e6b31e00b709502b0bff6e78_720.jpg

aea8009a2bfa46801ef8c2d9be2f21ae_720.jpg


