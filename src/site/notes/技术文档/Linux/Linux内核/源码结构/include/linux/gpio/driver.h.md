---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h/","dg-note-properties":{}}
---

# struct gpio_chip
一般调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib.c#gpiochip_add_data_with_key\|gpiolib.c#gpiochip_add_data_with_key]]函数注册到内核的`GPIO`子系统的设备列表中

包括下述成员:
- `of_xlate`: 用于依赖`GPIO`子系统的设备驱动引用`GPIO`时的控制器匹配
	- 如果芯片厂商没有自定义, 一般会使用`GPIO`子系统里默认的[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib-of.c#of_gpio_simple_xlate()\|gpiolib-of.c#of_gpio_simple_xlate()]]


# gpiochip_add_data宏
实际是对[[技术文档/Linux/Linux内核/源码结构/drivers/gpio/gpiolib.c#gpiochip_add_data_with_key\|gpiolib.c#gpiochip_add_data_with_key]]函数的封装

一般由芯片厂商填充[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip\|#struct gpio_chip]], 并调用此函数, 比如下述示例:
- `STM32`
	- 填充在[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c#stm32_gpio_template变量\|pinctrl-stm32.c#stm32_gpio_template变量]]
	- 调用在[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c#stm32_gpiolib_register_bank()\|pinctrl-stm32.c#stm32_gpiolib_register_bank()]]