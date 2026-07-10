---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c/","dg-note-properties":{}}
---

# stm32_gpio_template变量

# stm32_pctrl_ops变量

包括下述实例:
- `dt_node_to_map`: 参考函数[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c#stm32_pctrl_dt_node_to_map()\|#stm32_pctrl_dt_node_to_map()]]

# struct stm32_pinctrl
继承自`pinctrl_desc`的子类

# stm32_pctl_probe()
`pinctrl`子系统初始化函数, 在被注册为平台驱动的具体的芯片型号的`.c`文件里引用, 比如[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32mp157.c\|pinctrl-stm32mp157.c]]

主要负责下述工作:
1. 判断具体匹配的是兼容设备表里的哪个设备, 并返回匹配到的设备及其私有数据
	- 调用[[技术文档/Linux/Linux内核/源码结构/include/linux/of_device.h#of_match_device()\|of_device.h#of_match_device()]]函数
	- 私有数据参考[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32mp157.c#stm32mp157_pctrl_match变量\|pinctrl-stm32mp157.c#stm32mp157_pctrl_match变量]]
2. 获取设备节点的`pins-are-numbered`属性
3. 分配一块内核堆内存空间给`pctl`
4. 遍历`pinctrl`节点
	1. 如果子节点中有包含`gpio-controller`属性, 则注册为`GPIO`控制器设备节点
		- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c#stm32_gpiolib_register_bank()\|#stm32_gpiolib_register_bank()]]
	2. 注册失败, 则删除设备节点
		- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/of/dynamic.c#of_node_put()\|dynamic.c#of_node_put()]]
# stm32_gpiolib_register_bank()
包括下述工作:
1. 注册`GPIO`控制器到`GPIO`子系统中
	- 调用[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#gpiochip_add_data宏\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#gpiochip_add_data宏]]
2. 获取设备树属性`gpio-ranges`中索引为`0`的`phandle`指向的节点以及参数
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/of/base.c#of_parse_phandle_with_fixed_args()\|base.c#of_parse_phandle_with_fixed_args()]]

# stm32_pctrl_dt_node_to_map()