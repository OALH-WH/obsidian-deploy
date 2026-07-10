---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c/","dg-note-properties":{}}
---

# struct regulator_supply_alias
管理`supply`名称以及别名字符串
管理`dev`指针以及别名指针

包括下述成员:
- `src_dev`
- `src_supply`
- `alias_dev`
- `alias_supply`
# regulator_supply_alias_list变量
管理`supply`别名

# `_regulator_get()`
包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#regulator_dev_lookup()\|#regulator_dev_lookup()]]


# regulator_dev_lookup()

**返回值**
- 类型为[[技术文档/Linux/Linux内核/源码结构/include/linux/regulator/driver.h#struct regulator_dev\|struct regulator_dev]]

包括下述工作:
1. 如果`alias_supply`存在, 即用`alias_supply`和`alias_dev`
	1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#regulator_supply_alias()\|#regulator_supply_alias()]]
2. 在`dev`节点以及它的子节点查找后缀为`-supply`的`phandle_name`属性, 并返回引用的节点
	1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#of_get_regulator()\|#of_get_regulator()]]
3. 引用的节点存在, 就调用[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/of_regulator.c#of_find_regulator_by_node()\|of_regulator.c#of_find_regulator_by_node()]]


# regulator_supply_alias()
包括下述工作:
1. 判断是否找到别名`map`
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#regulator_find_supply_alias()\|#regulator_find_supply_alias()]]
2. 找到了就把当前`dev`和`supply`替换为`alias_dev/supply`
# regulator_find_supply_alias()
包括下述工作:
1. 遍历[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#regulator_supply_alias_list变量\|#regulator_supply_alias_list变量]], 查找匹配的`supply`
	1. 返回值类型为[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#struct regulator_supply_alias\|#struct regulator_supply_alias]]


# of_get_regulator()
包括下述工作
1. 给`supply`字符串加上后缀`-supply`
2. 获取不带参数的`phandle_name`属性引用的节点指针
	1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/of/base.c#of_parse_phandle()\|base.c#of_parse_phandle()]]
	2. 参数`index`为`0`
3. 如果没找到`phandle_name`引用的节点
	1. 去当前节点的子节点继续遍历查找
		1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/regulator/core.c#of_get_child_regulator()\|#of_get_child_regulator()]]
4. 找到了节点就返回这个节点

# of_get_child_regulator()
