---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/gpio/gpio.txt/","dg-note-properties":{}}
---

# 引用GPIO控制器
## 属性
### `[CUSTOM_NAME-]gpios`
**示例**
```devicetree
	gpio1: gpio1 {
		gpio-controller;
		#gpio-cells = <2>;
	};
	[...]

	data-gpios = <&gpio1 12 0>,
		     <&gpio1 13 0>,
		     <&gpio1 14 0>,
		     <&gpio1 15 0>;
```


# 定义GPIO控制器

# 属性
## `#gpio-cells`
规定如何引用`gpio`

值应该为`2`
`eg. #gpio-cells = <2>;`
## `gpio-ranges`
这个属性的意思是把在`pinctrl`的引脚映射到`gpio`控制器里

一个示例:
- `gpio-ranges = <&foo 0 20 10>, <&bar 10 50 20>;`
它的意思是:
- pins 20..29 on pin controller "foo" is mapped to GPIO line 0..9 and
- pins 50..69 on pin controller "bar" is mapped to GPIO line 10..29

 **基本格式**
```
<[pin controller phandle], [GPIO controller offset],
                [pin controller offset], [number of pins]>;
```