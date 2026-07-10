---
{"dg-publish":true,"permalink":"/技术文档/构建工具/kconfig/KConfig/","dg-note-properties":{}}
---

- KConfig一般有以下几个知识点

	- config模块

	- menuconfig模块

	- menu模块

	- choice模块

	- if 和 depends on 模块

- 菜单项

```
1. config ARCH_AIROHA 
2.     bool "选项名" 
3.     depends on ARCH_MULTI_V7 
4.     select ARM_AMBA 
5.     default n 
6.     help 
7.       Support for Airoha EN7523 SoCs
```

	- config: 表示一个选项

	- ARCH_AIROHR: 句柄，可用于控制MakeFile， 选择编译方式

	- bool： 选择可能，TRUE表示选中，FALSE表示不选中，选中则编译，否则不编译

	- depends on: 依赖，后面的选择被选择后，这个选项才能被选

	- select：当前选项选中后，则select后指定的选项自动被选择

	- default：缺省配置项

	- help：帮助信息

- 菜单属性

	- 类型定义

```
config BSP_USING_WDT
	bool "Enable Watchdog Timer"
	select RT_USING_WDT
	default n
```

		- 菜单选项可以有多个属性，并不要求这些属性可以用在任何地方。**每个配置选项都必须指定类型。**在5种类型中 tristate 和 string 为基本类型，其他类型都是基于这两个基本类型。

		- tristate三态类型：取值范围为Y/N/M，相较bool类型，tristate类型的菜单项多了一个编译成内核模块的选项。

		- string字符串：默认菜单选项显示对应字符串

		- 示例

```
config RT_CONSOLE_DEVICE_NAME
	string "the device name for console"
	default "uart1"
```

		- result展示：

![](WEBRESOURCE273ed778b0886fc14e4ae05545b03e56image.png)

		- integer整型

		- 示例

```
config BSP_I2C1_SCL_PIN
	int "I2C1 scl pin number"
	range 1 176
	default 116
```

		- result展示：

![](WEBRESOURCE71e7ee0364effa5a61bc8fffcf0e8385image.png)

		- prompt：输入提示

		- 示例

```
   bool "Networking support"
和
   bool
   prompt "Networking support"
等价
```

		- default：默认值

		- depends：依赖关系