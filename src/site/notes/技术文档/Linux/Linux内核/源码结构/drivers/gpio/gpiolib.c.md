---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib.c/","dg-note-properties":{}}
---

# gpio_devices变量
一个链表表头, 用于把所有`GPIO`控制器串联起来

# fwnode_get_named_gpiod()
主要包括下述工作:
1. 判断设备节点是否是**设备树节点**
	1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#gpiod_get_from_of_node()\|gpiolib-of.c#gpiod_get_from_of_node()]]函数, 继续解析节点信息
# gpiochip_find()

**参数**
- `data`: 空指针类型, 要传递给`match`的数据
- `match`: 函数指针, 类型为`int (*)(struct gpio_chip *chip, void *data)`
**返回值**
- 一个指针, 类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip]]

包括下述工作:
1. 遍历`GPIO`控制器的列表, 匹配到目标`GPIO`控制器就`break`
	- 元素类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/gpiolib.h#struct gpio_device\|gpiolib.h#struct gpio_device]]
2. 


# gpiochip_add_data_with_key
用于注册`GPIO`控制器到[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib.c#gpio_devices变量\|#gpio_devices变量]]中, 一般由芯片厂商的驱动使用注册

比如在[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c#stm32_gpiolib_register_bank()\|pinctrl-stm32.c#stm32_gpiolib_register_bank()]]中会调用此函数注册`GPIO`控制器

包括下述工作:
1. 
