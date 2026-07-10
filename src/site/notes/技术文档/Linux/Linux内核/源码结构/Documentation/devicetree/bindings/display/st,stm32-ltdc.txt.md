---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/display/st,stm32-ltdc.txt/","dg-note-properties":{}}
---

# 基本属性
- `compatible`
- `reg`
- `clocks`
- `clock-names`
- `resets`: 重置为给设备使用(用`RCC`宏来定义)
# 基本节点
- `port`: 表示显示接口输出的位置, 最多两种输出端点
	- `endpoint`: 参考[[技术文档/常见硬件模块/显示模块/基本知识#接口类型\|基本知识#接口类型]]
		- 用于外部`GRB DSI`的显示屏/桥片设备, 使用`GPIO`输出
		- 用于`MIPI DSI`控制器的内部`DSI`的输入


# 示例
## RGB panel
```devicetree
/ {
	...
	soc {
	...
		ltdc: display-controller@40016800 {
			compatible = "st,stm32-ltdc";
			reg = <0x40016800 0x200>;
			interrupts = <88>, <89>;
			resets = <&rcc STM32F4_APB2_RESET(LTDC)>;
			clocks = <&rcc 1 CLK_LCD>;
			clock-names = "lcd";

			port {
				ltdc_out_rgb: endpoint {
				};
			};
		};
	};
};
```