---
{"dg-publish":true,"permalink":"/技术文档/RTOS/RT-Thread/CubeMX配置/","dg-note-properties":{}}
---

1. CubeMX_Config

1. Inc

1. stm32h7xx_hal_conf.h：负责使能对应的外设模块

1. stm32h7xx_it.h:中断处理，由于rt有自己的中断处理方法，因此不包含此文件

1. Src

1. stm32h7xx_hal_msp.c:负责重写MspInit函数

1. msp init不用手动调用，会自动调用（在哪？暂时不知道）

1. main.c

1. 有系统时钟树初始化函数，替换driver/drv_clk.c中使用的时钟树初始化函数

1. 配置问题

1. 定义问题,找不到stm32h7xx_hal_def.h中的定义了

1. 解决方案

1. 要用hal库的内容,直接包含stm32h7xx_hal.h 就可以了,不能直接越级包含其他层级的头文件

1. 找不到stm32h7xx_hal_conf.h

1. 解决方案

1. 某个文件include 这个文件之前要先嵌套包含其依赖文件

1. 或者干脆不包含这个文件，参考其他类似文件的include