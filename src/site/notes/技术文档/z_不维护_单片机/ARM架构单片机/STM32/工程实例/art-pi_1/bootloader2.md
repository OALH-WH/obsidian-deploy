---
{"dg-publish":true,"permalink":"/技术文档/z_不维护_单片机/ARM架构单片机/STM32/工程实例/art-pi_1/bootloader2/","dg-note-properties":{}}
---

1. 常见问题及解决方案

1. bootloader2没重定向VTOR,导致程序不能正常工作

1. 解决方案

1. 默认工程模板是从内部flash启动,因此中断向量表默认指向内部flash映射到CPU地址空间的首地址上

1. 需要手动重定向到当前程序烧录的物理存储空间在CPU地址空间的首地址上