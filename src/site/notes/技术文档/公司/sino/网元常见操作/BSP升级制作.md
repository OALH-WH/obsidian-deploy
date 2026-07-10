---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/网元常见操作/BSP升级制作/","dg-note-properties":{}}
---

- 升级前准备

- 查看是否支持overlay

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E7%BD%91%E5%85%83%E5%B8%B8%E8%A7%81%E6%93%8D%E4%BD%9C/images/WEBRESOURCEf97aae3aca75f38e932fbb0a199b139bimage.png)

- 查看bsp版本

	- 查看uboot 环境变量

		- fw_printenv

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E7%BD%91%E5%85%83%E5%B8%B8%E8%A7%81%E6%93%8D%E4%BD%9C/images/WEBRESOURCE18cb878f0a094e79798a5d4df9f01dbcimage.png)

1. 单个升级

1. 制作工具的使用

1. -n: 清理并生成target

1. -p: 制作

1. BSP制作

1. 解压上一个版本的bsp升级包

1. 更新spec目录下信息

1. 进入spec目录查看对应板卡的分区情况以及uboot,kernel版本等信息,并更新

1. 更新flash目录下的文件

1. 更新的spec目录替换掉工具中的spec目录

1. firmware_make -n：生成包含了更新的spec目录的target目录

1. 再把flash目录移到target目录中

1. firmware_make -p：制作bsp升级包