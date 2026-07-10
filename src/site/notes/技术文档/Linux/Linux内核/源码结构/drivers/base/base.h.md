---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/base/base.h/","dg-note-properties":{}}
---


# driver_match_device()
包括下述工作:
1. 调用`drv->bus->match`回调函数去匹配
	- 比如平台总线匹配参考[[技术文档/Linux/Linux内核/源码结构/drivers/base/platform.c#platform_bus_type变量\|platform.c#platform_bus_type变量]]