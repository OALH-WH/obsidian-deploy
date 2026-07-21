---
{"dg-publish":true,"permalink":"/技术文档/个人项目开发笔记/MP157Mini开发笔记/驱动开发/I2C设备驱动/","dg-note-properties":{}}
---

# ap3216c

## 硬件资料
从机`i2c`从机地址为`0x1e`
## 设备驱动
## 设备树

**节点描述**
`i2c`适配器节点描述参考[[技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/i2c/i2c-stm32.txt\|i2c-stm32.txt]]

**步骤**
1. `i2c5`添加设备子节点`ap3216c`
	1. 添加`compatible`属性, 用于匹配驱动
	2. 添加`reg`属性, 用于设置`i2c`设备从机地址
		1. 设备地址可通过设备数据手册获取
		2. 参考[[技术文档/个人项目开发笔记/MP157Mini开发笔记/驱动开发/I2C设备驱动#硬件资料\|#硬件资料]]
2. 


**示例**
```devicetree
// 上述步骤1
&i2c5 {

    ap3216c: i2c51@1e {

        compatible = "ap3216c";

        reg = <0x1e>

    }

};




```