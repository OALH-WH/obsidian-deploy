---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/二进制程序相关/readelf命令/","dg-note-properties":{}}
---

# 背景
- 查看可执行程序的信息
- 静态分析, 不会执行程序
# 参数
- `-l`: 显示程序头信息
	- 动态链接器路径
- `-s`: 显示符号表, 参考[[技术文档/Linux/linux常用操作/二进制程序相关/符号表\|符号表]]
- `-d`: 显示动态库信息