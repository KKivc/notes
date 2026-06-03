---
title: PWR
source: feishu
space: STM32
---

PWR
简介
电源控制
负责管理STM32内部的电源供电部分，实现可编程电压监测器、低功耗模式功能
可编程电压监测器（PVD）可以监控VDD电源电压，当VDD下降到DVD阈值以下或上升到DVD阈值之上时，PVD触发中断
低功耗模式：睡眠模式、停机模式、待机模式，在系统空闲时，降低STM32的功耗，延长设备使用时间
低功耗模式
image.png

执行WFI/WFE指令后，进入低功耗模式
WFI进入睡眠模式，可被任意一个NVIC响应的中断唤醒
WFE进入睡眠模式，可被唤醒事件唤醒
image.png



