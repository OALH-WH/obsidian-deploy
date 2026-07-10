---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/devicetree.c/","dg-note-properties":{}}
---

# pinctrl_dt_to_map()

包括下述工作:
1. 循环查找此设备节点的属性是否存在`pinctrl-0`, `pinctrl-1`, `...`诸如此类的属性名, 从`pinctrl-0`开始查找
	1. 如果`pinctrl-0`都不存在, 则直接**退出函数**
	2. 在`pinctrl-`前缀的属性存在的基础上, 判断`pinctrl-names`属性是否存在
	3. 如果存在获取其值, 不存在则使用默认值, 比如`pinctrl-0`的`0`
	4. 解析引用的`pinctrl device`
		- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/devicetree.c#dt_to_map_one_config()\|#dt_to_map_one_config()]]


# dt_to_map_one_config()
用于映射配置

包括下述工作:
1. 调用回调函数`ops->dt_node_to_map`
	- 比如`STM32`, 指向的函数定义在[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c#stm32_pctrl_ops变量\|pinctrl-stm32.c#stm32_pctrl_ops变量]]