---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h/","dg-note-properties":{}}
---

# enum gpiod_flags
用于配置`GPIO`的方向和输出的值 , 这些值不能**或**, 包括下述枚举:
- `GPIOD_ASIS`: 保持方向和值不变
- `GPIOD_IN`
- `...`

# gpiod_put()
定义在`drivers/gpio/gpiolib.c`


# devm_gpiod_get()
定义在`drivers/gpio/gpiolib-devres.c`

**参数**


# devm_fwnode_get_gpiod_from_child()

对于引用了`GPIO`设备节点的设备, 可以使用此函数获取`GPIO`的资源, 比如使用了`gpios/gpio`作为后缀的属性

实际调用[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h#devm_fwnode_get_index_gpiod_from_child()\|#devm_fwnode_get_index_gpiod_from_child()]], `index`参数默认为`0`
# devm_fwnode_get_index_gpiod_from_child()
定义在[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-devres.c#devm_fwnode_get_index_gpiod_from_child\|gpiolib-devres.c#devm_fwnode_get_index_gpiod_from_child]]

**参数**
- `dev`: `GPIO`子系统的消费者
	- 一般为`GPIO`设备驱动
- `con_id`
	- 一般为`NULL`
- `index`: 比如当设备树的`gpios`属性有多个`GPIO`的时候, 此值表示索引哪个
	- 从`0`开始索引
- `child`: 子设备节点的句柄, 用于获取`GPIO`信息
- `flags`: 配置gpio的输出方向和值
	- 一般为`GPIOD_ASIS`
	- 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h#enum gpiod_flags\|#enum gpiod_flags]]
- `label`: 为获取到的GPIO设置一个描述性标签，该标签会显示在 `/sys/kernel/debug/gpio` 等调试接口中，便于识别用途。
	- 一般为`NULL`

**返回值**
[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/gpiolib.h#struct gpio_desc\|gpiolib.h#struct gpio_desc]]类型的指针