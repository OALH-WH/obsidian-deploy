---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h/","dg-note-properties":{}}
---

# struct i2c_adapter

包括下述成员:
- `algo`: [[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_algorithm\|#struct i2c_algorithm]]指针类型, 提供访问总线的接口实现

# struct i2c_algorithm
提供`i2c`适配器和设备之间通信的接口实现

如果一个`i2c`适配器提供的接口不支持`i2c`级别的访问, 则设置`master_xfer`为`null`

包括下述成员:
- `master_xfer`: 发起一个`i2c`事务组到给定的`i2c`适配器, 
	- 由`adap`指定`i2c`适配器
	- 由`msgs`数组定义事务
	- 由`num`定义有效事务数量