---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/df命令/","dg-note-properties":{}}
---

# 背景
- 和 `lsblk`命令的区别
	- `lsblk`命令读的是块设备上的实际信息
	- `df`命令读的是系统层面所使用的信息
# 使用
# 内容解析
## 行
## 列
- `Filesystem`: 使用的文件系统
	- `udev`: 虚拟文件系统, 存储位置为内存空间, 标识这是一个由udev管理的tmpfs, 参考[[技术文档/Linux/linux常用操作/设备管理/udev设备管理\|udev设备管理]]
	- `tmpfs`: 虚拟文件系统, 使 存储位置为内存空间, 因此 `lsblk`命令是读不到的
	- `/dev/mapper/debian12--vg-root`: 使用LVM管理划分的逻辑卷, 在 `lsblk`命令中读到的是实际格式化到块设备上的文件系统类型
- `Size`
- `Used`
- `Avail`
- `Use%`
- `Mounted on`: 挂载点
