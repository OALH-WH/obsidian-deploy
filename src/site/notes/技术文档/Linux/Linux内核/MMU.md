---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/MMU/","dg-note-properties":{}}
---

# 背景
- 内存管理单元
- 用于物理内存到虚拟内存的映射
	- 虚拟内存的大小只跟芯片的架构相关, 比如32位架构的芯片, 虚拟内存大小就是`2*32` bit = `4`GB