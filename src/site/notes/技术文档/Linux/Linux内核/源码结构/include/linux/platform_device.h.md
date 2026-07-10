---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/platform_device.h/","dg-note-properties":{}}
---

# struct platform_driver
平台驱动类, 继承自`structr driver`, 包含下述成员:
- `probe`: 当和设备匹配成功之后, 会执行这个函数完成设备初始化, 和资源分配
- `driver`: 父类, 定义在[[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#\|device.h#]]
# module_platform_driver宏
- 相当于对在驱动注册函数和卸载函数中分别调用了平台驱动注册和卸载函数

# struct platform_device
平台设备类, 是继承自`struct device`的子类, 包括下述成员:
- `dev`: 父类, 定义在[[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#\|device.h#]]


# platform_driver_register宏
实际调用的[[技术文档/Linux/Linux内核/源码结构/drivers/base/platform.c#__platform_driver_register()\|platform.c#__platform_driver_register()]]





# 解析平台设备结构体
`device_get_child_node_count`
- 解析