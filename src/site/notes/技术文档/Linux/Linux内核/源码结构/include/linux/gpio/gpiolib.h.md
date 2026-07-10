---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/gpio/gpiolib.h/","dg-note-properties":{}}
---

# gpio_suffixes变量
用于设备树和`ACPI`查找, 定义了下述后缀:
- `gpios`
- `gpio`


# struct gpio_desc

# struct gpio_device
包括下述成员:
- `chip`: 
	- 类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/driver.h#struct gpio_chip]]