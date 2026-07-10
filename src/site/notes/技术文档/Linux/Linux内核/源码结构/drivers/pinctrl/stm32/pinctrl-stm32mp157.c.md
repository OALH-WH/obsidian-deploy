---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32mp157.c/","dg-note-properties":{}}
---


# stm32mp157_pins变量
定义了所有`pin`的信息, 类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/pinctrl/stm32/pinctrl-stm32.h#struct stm32_pinctrl_match_data\|pinctrl-stm32.h#struct stm32_pinctrl_match_data]]



# stm32mp157_pctrl_match变量
设备兼容表变量, 定义了用于兼容匹配设备的`compatible`及其私有数据

包含下述`compatible`:
- `st,stm32mp157-pinctrl`
	- 私有数据参考[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32mp157.c#stm32mp157_pins变量\|#stm32mp157_pins变量]]
- `st,stm32mp157-z-pinctrl`


