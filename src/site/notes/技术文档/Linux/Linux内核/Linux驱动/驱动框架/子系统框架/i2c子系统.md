---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/i2c子系统/","dg-note-properties":{}}
---

# 子系统框架
![Pasted image 20260710095723.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/Linux%E5%86%85%E6%A0%B8/Linux%E9%A9%B1%E5%8A%A8/%E9%A9%B1%E5%8A%A8%E6%A1%86%E6%9E%B6/%E5%AD%90%E7%B3%BB%E7%BB%9F%E6%A1%86%E6%9E%B6/resources/Pasted%20image%2020260710095723.png)
# 子系统组成
## I2C core, I2C核心
## I2C adapter, I2C总线驱动
一般都是由半导体厂商维护
`ST`厂商参考[[技术文档/Linux/Linux内核/源码结构/drivers/i2c/busses/i2c-stm32f7.c\|i2c-stm32f7.c]]

两个重要的结构体:
- `i2c_adapter`: 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_adapter\|i2c.h#struct i2c_adapter]]
- `i2c_algorithm`: 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_algorithm\|i2c.h#struct i2c_algorithm]]

主要工作:
1. 初始化 `i2c_adapter` 结构体变量，然后设置 `i2c_algorithm` 中的 `master_xfer` 函数
2. 完成以后通过 `i2c_add_numbered_adapter`
或`i2c_add_adapter`这两个函数向`I2C` 子系统注册设置好的`i2c_adapter`
3. 总线驱动的删除通过`i2c_del_adapter`
## I2C client, I2C设备驱动

重要的结构体:
- `i2c_client`: 一个 `I2C` 设备对应一个 `i2c_client` 结构体变量，系统每检测到一个 `I2C`从设备就会给这个设备分配一个 `i2c_client`
	- 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_client\|i2c.h#struct i2c_client]]
- `i2c_driver`: 类似 platform_driver 
	- 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/i2c.h#struct i2c_driver\|i2c.h#struct i2c_driver]]

主要工作:
1. `i2c_set_clientdata`用来设置私有数据
2. `i2c_get_clientdata`用来获取私有数据
3. `i2c_register_driver/i2c_add_driver`注册驱动
4. `i2c_`
5. `i2c_del_driver`注销驱动


# 设备树
`i2c`子系统所有相关文档参考[[技术文档/Linux/Linux内核/源码结构/Documentation/i2c/index.rst\|index.rst]]
`i2c`适配器节点描述参考[[技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/i2c/i2c-stm32.txt\|i2c-stm32.txt]]

# 示例
## i2c从设备驱动
```c

```


## 