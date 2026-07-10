---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/base/dd.c/","dg-note-properties":{}}
---


# driver_probe_device()

包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/dd.c#really_probe()\|#really_probe()]]

# really_probe()
包括下述工作:
1. 如果使用了`pinctrl`, 在驱动匹配成功设备进行初始化之前, 先绑定`pins`
	- 调用了[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/pinctrl.c#pinctrl_bind_pins()\|pinctrl.c#pinctrl_bind_pins()]]


# driver_attach()

包括下述工作
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/bus.c#bus_for_each_dev()\|bus.c#bus_for_each_dev()]]函数, 参数`fn`指定为[[#`__driver_attach()`]]
# `__driver_attach()`
包括下述工作: 
1. 匹配驱动和设备
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/base.h#driver_match_device()\|base.h#driver_match_device()]]
2. 匹配成功后初始化设备
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/dd.c#driver_probe_device()\|#driver_probe_device()]]