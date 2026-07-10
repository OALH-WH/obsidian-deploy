---
{"dg-publish":true,"permalink":"/技术文档/个人项目开发笔记/MP157Mini开发笔记/Uboot/","dg-note-properties":{}}
---

1. 通用的bootloader，支持多种架构

1. 步骤

1. uboot源码的获取

1. 第三方开发板厂商就使用开发板厂商提供的uboot源码编译

1. 芯片半导体厂商就使用半导体厂商提供的uboot源码编译

1. 编译

1. make distclean

1. make ARCH=[arm] CROSS_COMPILE=[交叉编译器前缀] [stm32mp15_trusted_defconfig eg./configs/stm32mp15_trusted_defconfig]

1. make DEVICE_TREE=[stm32mp157d-evl //./arch/arm/dts/stm32mp157d-evl]