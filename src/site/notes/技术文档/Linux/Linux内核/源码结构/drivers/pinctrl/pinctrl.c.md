---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/pinctrl.c/","dg-note-properties":{}}
---

# pinctrl_bind_pins()
包括下述工作:
1. 获取`pinctrl`
	- 调用了[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c#devm_pinctrl_get()\|技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c#devm_pinctrl_get()]]函数