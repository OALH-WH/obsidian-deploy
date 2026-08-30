---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/platform_device.h/","dg-note-properties":{}}
---

# struct platform_driver
平台驱动类, 继承自`structr driver`, 包含下述成员:
- `probe`: 当和设备匹配成功之后, 会执行这个函数完成设备初始化, 和资源分配
- `remove`: 驱动卸载或者热插拔时触发, 一般用于释放软件资源, 可能涉及硬件资源的释放(主要根据具体硬件)
- `shutdown`: 系统关机或重启时调用, 一般用于释放硬件资源
- `suspend`: 成员废弃, 进入休眠时调用, 一般保存寄存器值、关闭时钟、关中断
- `resume`: 成员废弃, 退出休眠时调用, 一般恢复寄存器、重开时钟、重新配置硬件
- `driver`: 父类, 定义在[[技术文档/Linux/Linux内核/源码结构/include/linux/device.h\|device.h]]
`suspend/resume`现代推荐使用`SIMPLE_DEV_PM_OPS()`注册
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