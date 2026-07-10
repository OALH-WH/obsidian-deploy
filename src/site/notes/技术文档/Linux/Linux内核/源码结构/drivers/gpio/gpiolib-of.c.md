---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c/","dg-note-properties":{}}
---

# gpiod_get_from_of_node()
包括下述工作:
1. 使用`GPIO`的`API`获取`GPIO`描述和标志
	- 调用了[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#of_get_named_gpiod_flags()\|#of_get_named_gpiod_flags()]]函数
2. 

# of_get_named_gpiod_flags()
包括下述工作: 
1. 获取指定属性引用的节点以及它的参数信息
	- 比如获取`gpios`某个`index`指向的`GPIO`节点和它的参数数量以及每个参数的值
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/of/base.c#of_parse_phandle_with_args_map()\|base.c#of_parse_phandle_with_args_map()]]函数
2. 匹配`GPIO`控制器, 获取对应[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip]]类型的数据
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#of_find_gpiochip_by_xlate()\|#of_find_gpiochip_by_xlate()]]函数
	- 返回值类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip]]
3. 获取单个`GPIO`描述信息及其`flags`
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#of_xlate_and_get_gpiod_flags()\|#of_xlate_and_get_gpiod_flags()]]

# of_find_gpiochip_by_xlate()
包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib.c#gpiochip_find()\|gpiolib.c#gpiochip_find()]]函数
	1. 匹配函数为[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#of_gpiochip_match_node_and_xlate()\|#of_gpiochip_match_node_and_xlate()]]
	2. 数据为`phandle`的节点及参数数据

# of_gpiochip_match_node_and_xlate()

**参数**
- `chip`: 用于匹配`GPIO`控制器, 类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip]]
- `data`: 用来存储`phandle`的节点和参数信息

包括下述工作:
1. 比较三种情况, 都满足就返回`true`, 否则返回`false`
	1. 比较`chip`中的设备节点指针和`phandle`中的设备节点指针指向的地址是否相同
	2. `chip`中的`of_xlate`回调函数指针是否不为空
	3. 调用`of_xlate`回调函数, 返回值是否`>=0`

# of_xlate_and_get_gpiod_flags()
获取`GPIO`的`flags`和描述信息

**参数**
- `chip`: `GPIO`控制器
- `gpiospec`: 包括`GPIO`控制器的节点和参数信息 
- `flags`: 将会被填充的

**返回值**
- `desc`: 单个`GPIO`描述信息

包括下述工作:
1. 获取单个`GPIO`对应的`flags`
	- 调用`chip->of_xlate`回调函数, 参考[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#of_gpio_simple_xlate()\|#of_gpio_simple_xlate()]]
	- 返回引用`GPIO`的第一个参数, 一般表示`GPIO`的引脚索引
2. 获取单个`GPIO`描述
	-  调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#gpiochip_get_desc()\|#gpiochip_get_desc()]]

# gpiochip_get_desc()
包括下述工作:
1. 

# of_gpiochip_add()
包括下述工作:


# of_gpio_simple_xlate()
如果芯片厂商没有自定义, 则将会使用此函数