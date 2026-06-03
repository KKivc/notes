---
title: WDG
source: feishu
space: STM32
---

WDG
简介
看门狗
监控程序运行状态，程序出现卡死/跑飞现象时，看门狗能及时复位程序
本质是一个定时器，当指定时间内，程序没有执行喂狗(重置计数器)时，看门狗硬件电路自动产生复位信号
STM32内置两个看门狗：独立看门狗(IWDG):独立工作，对时间精度要求低 ；窗口看门狗(WWDG) :要求看门狗在精确计时窗口起作用
IWDG
超出时间：T=Tlsi x PR预分频系数 x （RL+1);Tlsi=1/40k
image.png


image.png

image.png

WWDG
image.png

image.png

image.png

区别
image.png


