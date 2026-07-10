---
{"dg-publish":true,"permalink":"/技术文档/Linux/系统启动错误处理/卡在initramfs/","dg-note-properties":{}}
---

1. blkid： 查看并识别磁盘、分区或文件系统的信息

1. fsck -t <fs type> <dev file>

1. -t：指定文件系统类型

1. dev file：设备文件名

1. 作用：修复文件系统中的错误

1. exit：重新启动系统