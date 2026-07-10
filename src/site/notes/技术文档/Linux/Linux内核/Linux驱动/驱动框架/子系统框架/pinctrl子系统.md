---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/pinctrl子系统/","dg-note-properties":{}}
---

# 背景
- 驱动实现基于[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/字符设备驱动框架/字符设备驱动框架\|字符设备驱动框架]], 字符设备驱动框架中提到的功能, 这里不再赘述
- 内核将`pinctrl`驱动抽象为一个`pinctrl_desc`对象, 而各个厂商的`pinctrl`驱动就是该对象的一个实例, 并将该实例注册到内核中
## 主要工作内容
- 获取设备树的`pin`信息
- 设置`pin`的复用功能, 通过结构体`struct pinmux_ops`实现
- 设置`pin`电气特性的配置, 比如上拉, 下拉, 速度等
- 设置`pin`的状态


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
