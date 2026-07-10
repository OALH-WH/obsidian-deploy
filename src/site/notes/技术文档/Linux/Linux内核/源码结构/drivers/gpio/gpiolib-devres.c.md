---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-devres.c/","dg-note-properties":{}}
---

# devm_fwnode_get_index_gpiod_from_child
做了下述工作:
1. 把`GPIO`资源和设备节点绑定
2. 遍历`GPIO`后缀, 查找属性
	- 定义的`GPIO`后缀参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/gpiolib.h#gpio_suffixes变量\|gpiolib.h#gpio_suffixes变量]]
3. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib.c#fwnode_get_named_gpiod()\|gpiolib.c#fwnode_get_named_gpiod()]]继续解析节点属性