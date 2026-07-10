---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/of.h/","dg-note-properties":{}}
---


# struct device_node

包括下述成员: 
- ``
# of_find_property()
根据属性名查找属性

**参数**
- `lenp`: 可选参数, 如果不为空, 返回属性值长度

**返回值**
- 成功, 返回找到的属性指针, 类型为`struct property *`
- 失败, 返回空指针

# of_match_node

# of_property_read_u32_array()

**参数**


**返回值**
- `0`: 成功
- `-EINVAL`: 属性不存在
- `-ENODATA`: 属性存在, 但没值
- `-EOVERFLOW`: 属性值存在, 但值无效