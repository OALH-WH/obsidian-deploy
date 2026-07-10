---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/pinctrl/pinctrl.h/","dg-note-properties":{}}
---

# struct pinctrl_desc
引脚控制器描述, 包括以下成员:
- `pmxops`: `strcut pinmux_ops`结构体指针, 指向引脚复用操作集合, 如果在你的驱动中支持引脚复用的话