---
title: C语言
source: feishu
space: STM32
---

C语言
关键字
char：8位               int8_t(typedef重新命名的变量类型)
Unsigned char：8位       uint8_t
short：16位                   int16_t
Unsigned short：16位         uint16_t
int：32位                    int32_t
Unsigned int：32位       uint32_t
long：32位
Unsigned long：32位
Long long：64位               int64_t
Unsigned long long：64       uint64_t
float：32位
Double：64位
const ：常量，只读，不能修改
stm32中，const定义的常量(要赋值)，是存储在Flash里，只读不写
原码00000001  正数：原码=反码=补码  原码最高位为1为负
反码（原码取反、表示负数） 11111110
补码11111111（反码加一）运算用它，高位补1、低位补0
16进制——>十进制：0x11：1x16^1 + 1x16^0
宏定义
关键字：#define
定义宏定义：#define ABC 12345   //新名字在左边
引用宏定义：int a = ABC；  //等效于int a = 12345
Typedef
将比较长的变量类型换名字，新名字在右边
定义typedef：typedef unsigned char uint8_t;
引用typedef：uint8_t a;
结构体
关键字：struct
数据打包，不同变量类型的集合

typedef struct{char x;
int y; 
float z;}StructName_t;  //定义结构体

StructName_t.x = 'A';
StructName_t.y = 66;
StructName_t.z = 1.25；  //定义结构体里的值，应用

   //pStructName为结构体的地址，写入
pStructName->x = 'A';
pStructName->y = 66;
pStructName->z = 1.23;
枚举
关键字：enum
定义一个取值受限制的整形变量，用于限制变量取值范围
不属于数据类型

typedef enum {monday = 1,   //用逗号隔开
tuesday,     //按顺序，自己增1
wednesday}week_t;

week_t week;
week = monday;  //week=1
week = tuesday  //week = 2
week = wednesday;
volatile:让主循环能“看见”中断已经发生的事件。主循环每次都真的走到信箱前看一次。
sizeof:计算内存占用大小
strlen：计算字符串长度
memset：<string.h>，把一段连续内存区域的每一个“字节”全部写成同一个值。
