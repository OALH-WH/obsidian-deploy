---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/pinctrl/pinmux.h/","dg-note-properties":{}}
---

# struct pinmux_ops
表示引脚复用操作集合, 包括以下成员:
- `get_functions_count`: 回调函数, 获取功能总数
- `get_function_name`: 获取功能名称
- `get_function_groups`: 获取功能组
- `strict`: 表示不允许使用同一个引脚的`GPIO`和其他复用功能, 在允许`pin`请求之前严格检查`gpio_owner`和`mux_owner`