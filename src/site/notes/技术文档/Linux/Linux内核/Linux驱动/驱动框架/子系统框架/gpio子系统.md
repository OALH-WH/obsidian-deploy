---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/gpio子系统/","dg-note-properties":{}}
---

# 背景
- 驱动实现基于[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/字符设备驱动框架/字符设备驱动框架\|字符设备驱动框架]], 字符设备驱动框架中提到的功能, 这里不再赘述
- 该子系统是依赖于`pinctrl`子系统的, 只有当`pinctrl`设置引脚为`gpio`模式, 才会用到`gpio`子系统的`API`
## 主要工作内容
- 设置初始化`GPIO`相关参数
- 提供相应的API函数
- 屏蔽掉了`GPIO`的设置过程, 方便了驱动开发者使用`GPIO`

# 结构体之间的关系
[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/resources/Drawing 2026-06-09 08.05.56.excalidraw\|Drawing 2026-06-09 08.05.56.excalidraw]]

# 设备资源解析API
**consumer.h**
给使用`GPIO`子系统的设备驱动(即`GPIO`子系统的消费者)提供`API`, 具体的参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h]], 常见的有:
- `devm_fwnode_get_index_gpiod_from_child`: 获取`gpio_desc`
	- 使用`fwnode`抽象层
- `devm_gpiod_get`: 获取`gpio_desc`
# 配置API

## 申请GPIO管脚
- `gpio_request`
## 释放GPIO管脚
- `gpio_free`
## 设置GPIO输入模式
- `gpio_direction_input`
## 设置GPIO输出模式
- `gpio_direction_output`
	- 1为高电平
## 获取GPIO的值
- `gpio_get_value`
## 设置GPIO的值
- `gpio_set_value`
