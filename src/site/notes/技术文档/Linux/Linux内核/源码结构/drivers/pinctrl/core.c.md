---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c/","dg-note-properties":{}}
---

# pinctrl_list变量
# devm_pinctrl_get()

包括下述工作:
1. 获取`pinctrl`
	- 调用了[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c#pinctrl_get()\|#pinctrl_get()]]

# pinctrl_get()

包括下述工作:
1. 查找`pinctrl`
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c#find_pinctrl()\|#find_pinctrl()]]
2. 没找到就创建它
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c#create_pinctrl()\|#create_pinctrl()]]

# find_pinctrl()

**参数**
- `dev`: 设备节点

包括下述工作:
1. 遍历[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/core.c#pinctrl_list变量\|#pinctrl_list变量]], 如果`dev`存在和`pinctrl_list`中保存的`pinctrl->dev`相同的, 则表示找到了, 返回这个`pinctrl`
	- 返回的类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/pinctrl/core.h#struct pinctrl\|core.h#struct pinctrl]]

# create_pinctrl()

包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/devicetree.c#pinctrl_dt_to_map()\|devicetree.c#pinctrl_dt_to_map()]]