---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/base/platform.c/","dg-note-properties":{}}
---

# 平台总线的定义
`struct bus_type platform_bus_type = {...}`

# 平台总线匹配

# struct bus_type

包括下述成员:
- `match`: 用于匹配驱动和设备

# platform_bus_type变量
类型参考[[技术文档/Linux/Linux内核/源码结构/drivers/base/platform.c#struct bus_type\|#struct bus_type]]

包括下述工作:
1. `match`函数指针指向[[技术文档/Linux/Linux内核/源码结构/drivers/base/platform.c#platform_match\|#platform_match]]函数
	- `match`调用的地方在[[技术文档/Linux/Linux内核/源码结构/drivers/base/base.h#driver_match_device()\|base.h#driver_match_device()]]

# __platform_driver_register()

包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/driver.c#driver_register()\|driver.c#driver_register()]]

## platform_match

函数的实现中, 有四种匹配机制:
- `OF`匹配, 即通过设备树匹配
- `ACPI`匹配
- `id_table`匹配, 即通过注册到平台总线的驱动结构体`platform_driver`的成员变量`id_table`匹配
- 直接比较驱动和设备结构体的成员变量`name`