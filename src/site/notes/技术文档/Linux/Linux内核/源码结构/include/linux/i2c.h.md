---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h/","dg-note-properties":{}}
---

# struct i2c_adapter

包括下述成员:
- `algo`: [[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_algorithm\|#struct i2c_algorithm]]指针类型, 提供访问总线的接口实现
- `nr`: 表示`i2c`适配器在系统中的序号, 比如`i2c-0`, `i2c-1`
- `dev`: [[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#struct device\|device.h#struct device]]类型指针

# struct i2c_algorithm
提供`i2c`适配器和设备之间通信的接口实现

如果一个`i2c`适配器提供的接口不支持`i2c`级别的访问, 则设置`master_xfer`为`null`

包括下述成员:
- `master_xfer`: 发起一个`i2c`事务组到给定的`i2c`适配器, 
	- 由`adap`指定`i2c`适配器
	- 由`msgs`数组定义事务
	- 由`num`定义有效事务数量

# struct i2c_client

包括下述成员:
- `dev`: [[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#struct device\|device.h#struct device]]类型
- `adapter`: [[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_adapter\|#struct i2c_adapter]]类型指针

# struct i2c_msg
用于[[技术文档/Linux/Linux内核/源码结构/drivers/i2c/i2c-core-base.c#i2c_transfer()\|i2c-core-base.c#i2c_transfer()]]函数, 实现主/从机之间传输数据

包括下述成员:
- `addr`: 从机地址, `7/10bits`
	- 如果使用`10bits`
		- `flags`必须设置`I2C_M_TEN`
		- 使用的`i2c`适配器必须支持`I2C_FUNC_10BIT_ADDR`
- `buf`: 要发送的字节数据
- `len`: 字节长度
- `flags`: 
	- `0`: 表示写数据
	- `I2C_M_RD`: 表示读数据
	- `I2C_M_TEN`: 表示使用`10bits`从机地址(**可选**)
	- `...`


# struct i2c_adapter
包括下述成员:

# struct i2c_driver

包括下述成员:
- `driver`: [[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#struct device_driver\|device.h#struct device_driver]]类型, 用于设备树设备节点的匹配
- `probe`: 设置匹配初始化函数
- `remove`: 


# i2c_register_driver()
向`i2c`总线注册`i2c`设备驱动
实现在[[技术文档/Linux/Linux内核/源码结构/drivers/i2c/i2c-core-base.c\|i2c-core-base.c]]

包括下述工作
1. 设置驱动所有者和总线类型为`i2c bus type`
2. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/driver.c#driver_register()\|driver.c#driver_register()]]
3. `debug`级别打印`driver->driver.name`成员

**参数**
- `owner`: 驱动所有者, 一般为`THIS_MODULE`
- `driver`: [[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_driver\|#struct i2c_driver]]类型指针


# i2c_del_driver()


# i2c_add_adapter()

实现在[[技术文档/Linux/Linux内核/源码结构/drivers/i2c/i2c-core-base.c\|i2c-core-base.c]]

包括下述工作:
1. 通过`aliases`属性, 获取`i2c`适配器静态`id`
	1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/of/base.c#of_alias_get_id()\|base.c#of_alias_get_id()]]函数
2. 否则自动从`0`分配一个最小可用的`id`
3. 设置`adapter->nr`为`id`

**参数**
- `adapter`: [[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_adapter\|#struct i2c_adapter]]类型指针