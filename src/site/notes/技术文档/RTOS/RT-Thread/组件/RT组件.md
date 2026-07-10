---
{"dg-publish":true,"permalink":"/技术文档/RTOS/RT-Thread/组件/RT组件/","dg-note-properties":{}}
---

1. fal组件

1. API

1. flash设备

1. 查找设备

1. fal_flash_device_find()

1. 分区相关

1. 查找flash分区

1. fal_partition_find

1. 获取分区表

1. fal_get_partition_table

1. 临时设置分区表

1. fal_set_partition_table_temp

1. 从分区读取数据

1. fal_partition_read

1. 往分区写入数据

1. fal_partition_write

1. 擦除分区的数据

1. fal_partition_erase

1.  擦除整个分区数据

1. fal_partition_erase_all

1. 打印分区表

1. fal_show_part_table

1. 基于分区创建设备

1. 创建blk设备

1. fal_blk_device_create

1. 创建mtd设备

1. fal_mtd_nor_device_create

1. 创建char设备

1. fal_char_device_create

1. 设备驱动框架

1. 设备驱动层：主要在libraries/drivers

1. 功能：负责驱动具体的硬件设备

1. 驱动框架层：主要在rt-thread/components/drivers

1. 功能：负责对某一类设备的共同特征提取抽象出来，并预留了不同的设备的独有特征。

1. 提供设备注册函数，负责把总线设备注册到rt thread的驱动中

1. I/O设备管理层

1. 功能：负责对上层软件提供统一的设备访问接口API

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/RTOS/RT-Thread/images/WEBRESOURCEe3742584700510757f001fcfc975e808image.png)