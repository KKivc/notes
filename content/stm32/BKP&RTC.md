---
title: BKP&RTC
source: feishu
space: STM32
---

BKP&RTC
BKP
备份寄存器
用于存储用户应用程序数据，当VDD电源被切断，他们仍然可以由VBAT维持供电
image.png

RTC
实时时钟
独立的定时器，为系统提供时钟和日历的功能
RTC和时钟配置系统处于后备区域，系统复位时数据不清零，当VDD电源被切断，他们仍然可以由VBAT维持供电
32位的可编程计数器，对应Unix时间戳的秒计数器
20位的可编程预分频器，适配不同频率的输入时钟
可选择三种RTC时钟源(RTCCLK)：HSE时钟除以128(通常为8M)、LSE振荡器时钟(通常32.768K)、LSI振荡器时钟(40K)
RTC引脚输出RTC校准时钟、RTC闹钟闹钟、秒脉冲
存储RTC时钟校准寄存器
用户数据存储容量：20字节(中小容量)/84字节(大容量)
image.png

BKP、RTC操作注意事项
时钟使能PWR、BKP
PWR备份访问开启使能
BKP写入
image.png


