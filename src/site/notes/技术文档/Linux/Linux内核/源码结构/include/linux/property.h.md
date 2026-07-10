---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/property.h/","dg-note-properties":{}}
---

# device_get_child_node_count()
获取设备子节点数量, 定义在`drivers/base/property.c`


# device_for_each_child_node()
遍历当前设备节点的子节点, 宏定义, 实现为一个不带代码块的`for`语句

**参数**
- `child`: 表示子节点句柄, 或者一个空句柄, `struct fwnode_handle`类型, 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/fwnode.h#struct fwnode_handle\|fwnode.h#struct fwnode_handle]]