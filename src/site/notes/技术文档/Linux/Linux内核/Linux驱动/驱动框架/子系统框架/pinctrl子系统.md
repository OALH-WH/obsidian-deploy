---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/pinctrl子系统/","dg-note-properties":{}}
---

# 背景
- 驱动实现基于[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/字符设备驱动框架/字符设备驱动框架\|字符设备驱动框架]], 字符设备驱动框架中提到的功能, 这里不再赘述
- 内核将`pinctrl`驱动抽象为一个`pinctrl_desc`对象, 而各个厂商的`pinctrl`驱动就是该对象的一个实例, 并将该实例注册到内核中
# 内核menuconfig配置

# 子系统组成
## pinctrl驱动

关键结构体和函数:
- `devm_pinctrl_register()`: 注册`pinctrl`


主要包括下述工作:
1. 

驱动实例参考:
- **ST**: 实现在`pinctrl`的驱动, 在`probe`中调用`devm_pinctrl_register()`
	- 参考[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c\|pinctrl-stm32.c]]


主要工作内容
- 获取设备树的`pin`信息
- 设置`pin`的复用功能, 通过结构体`struct pinmux_ops`实现
- 设置`pin`电气特性的配置, 比如上拉, 下拉, 速度等
- 设置`pin`的状态
# 消费者
驱动开发者一般不需要直接调用`pinctrl API`, `probe`时`driver core`自动调用
- `i2c`子系统参考[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/i2c子系统#I2C adapter, I2C总线驱动\|i2c子系统#I2C adapter, I2C总线驱动]]
	- 最终消费在[[技术文档/Linux/Linux内核/源码结构/drivers/base/dd.c#really_probe()\|dd.c#really_probe()]]
- `spi`子系统同上
- `gpio`子系统

# API
# 设备树

**示例**
```devicetree
```

--- 




# 结构体之间的关系

# 功能实现
## 把pinctrl驱动注册到内核
`pinctrl_register`

# 设备树实现

## 引脚控制器节点
参考`Documentation/devicetree/bindings/pinctrl/pinctrl-bindings.txt`, 说明了以下内容:
- 控制器节点该怎么调用
- 如何定义
- 有哪些属性

# 示例
