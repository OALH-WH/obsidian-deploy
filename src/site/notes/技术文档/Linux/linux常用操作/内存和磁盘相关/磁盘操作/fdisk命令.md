---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/fdisk命令/","dg-note-properties":{}}
---

# 作用
- 查看磁盘块和分区
- 设置分区

# 基本格式
`fdisk [options] [disk]`

**disk**
以人机交互界面控制磁盘块, 支持下述操作
- `p`: 打印分区表
- `n`: 新建分区, 选择下述配置
	- 分区号
	- 分区类型
	- 起始地址
	- 结束地址

**options**
- `-l`: 查看磁盘块和分区

# 实例
