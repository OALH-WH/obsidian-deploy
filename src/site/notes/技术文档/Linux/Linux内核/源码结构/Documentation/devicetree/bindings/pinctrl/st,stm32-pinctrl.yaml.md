---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/pinctrl/st,stm32-pinctrl.yaml/","dg-note-properties":{}}
---

# pinctrl设备节点

# gpio设备节点

**属性**
- `gpio-ranges`: 引用`pinctrl`设备节点
	- 参数固定为3个, 引用的节点数量可以是`[1,16]`
	- `eg. gpio-ranges=<&pinctrl 0 15 16>`