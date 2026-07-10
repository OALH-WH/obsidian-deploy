---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/of/base.c/","dg-note-properties":{}}
---

# of_match_node()
在设备匹配兼容表里查找指定设备节点

**参数**
- `matches`
- `node`: 指针, 指向的变量类型为[[技术文档/Linux/Linux内核/源码结构/include/linux/of.h#struct device_node\|of.h#struct device_node]]

**返回值**
- 兼容表的元素指针, 指针指向的类型为[[技术文档/Linux/Linux内核/源码结构/include/linux/mod_devicetable.h#struct of_device_id\|mod_devicetable.h#struct of_device_id]]

包括下述工作:
1. 调用[[#`__of_match_node()`]]


# `__of_match_node()`

包括下述工作:
1. 调用[[#`__of_device_is_compatible()`]]


# `__of_device_is_compatible()`
根据`compatible, type, name`按照最高优先级匹配

# of_parse_phandle_with_args_map()
在列表中查找由 phandle 指向的节点，并将该节点的指针重定向至包含列表的设备树节点中

此函数和`of_parse_phandle_with_args`函数不同的是, 这个`API`会在`phandle`指向的节点包括`<@stem_name>-map`属性时, 重映射一个`phandle`

用来解析`phandles`的列表和参数是非常有用的, 示例如下:
```cpp
/*
phandle1: node1 {
	#list-cells = <2>;
}
phandle2: node2 {
	#list-cells = <1>;
}
phandle3: node3 {
	#list-cells = <1>;
	list-map = <0 &phandle2 3>,
		   <1 &phandle2 2>,
		   <2 &phandle1 5 1>;
	list-map-mask = <0x3>;
};
node4 {
	list = <&phandle1 1 2 &phandle3 0>;
}

To get a device_node of the `node2' node you may call this:
of_parse_phandle_with_args(node4, "list", "list", 1, &args);

result:
	args.np        = node2   // 即 phandle2 指向的 device_node
	args.args_count = 1
	args.args[0]   = 3
*/
```

**参数**
- `np`: 包含`list`的设备树节点
- `list_name`: 列表名
- `stem_name`: 一个字符串前缀, 用于构成 `-map`, `-mask`, `-pass-thru` 等属性的名称。例如 `"gpio"` 会对应 `"gpio-map"`, `"gpio-map-mask"`, `"gpio-map-pass-thru"`
- `index`: 表示要解析的`list`中第几个节点的索引
- `out_args`: 一个指针, 存放解析的节点的参数

**返回值**
- 成功返回`0`, 并且填充`out_args`参数
- 失败返回一个错误码


# of_parse_phandle_with_fixed_args()


**参数**

**返回值**


# of_parse_phandle()
包括下述工作:
1. 获取没有参数的`phandle_name`属性引用的节点指针
	1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/of/base.c#__of_parse_phandle_with_args()\|#__of_parse_phandle_with_args()]]
	2. `eg. power-supply = <&v3v3>;`

# __of_parse_phandle_with_args()