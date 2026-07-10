---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/of_device.h/","dg-note-properties":{}}
---

# of_match_device()
用于匹配具体的设备, 定义在`drivers/of/device.c`

**参数**
- `matches`: 设备兼容表指针
- `dev`: 设备类指针

**返回值**
- 兼容表的元素类型指针
	- 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/mod_devicetable.h#struct of_device_id\|mod_devicetable.h#struct of_device_id]]
