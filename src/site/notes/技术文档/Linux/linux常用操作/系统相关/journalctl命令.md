---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/系统相关/journalctl命令/","dg-note-properties":{}}
---

# 背景
- 用于查看`systemd`管理的日志
- 也能查看内核日志
	- 因为它的用途就是用来统一管理系统日志, 也截获了`/dev/kmsg`的输出, 因此可以直接通过`journalctl -f -k`实时查看内核日志, 等同`dmesg -w`