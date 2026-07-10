---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/IP相关/arp命令/","dg-note-properties":{}}
---

# 作用
查看系统`ARP`表的内容
关于`ARP`的解释参考[[技术文档/计算机网络相关/OSI七层模型/链路层/协议/ARP协议\|ARP协议]]

# 基本格式

**可选参数**

**字段解析**
- `Address`: `IP`地址
- `HWtype`: 硬件类型, `eg. ether`(表示以太网接口)
- `HWaddress`: 硬件地址
	- `incompolete`: 表示地址解析失败
- `Flags Mask`
- `Iface`: 网络接口, `eg. eth2, eth0...`

# 实例
```shell
arp
```