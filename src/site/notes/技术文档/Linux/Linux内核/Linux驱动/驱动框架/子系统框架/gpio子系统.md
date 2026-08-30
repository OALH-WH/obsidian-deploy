---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/gpio子系统/","dg-note-properties":{}}
---

# 背景
- 驱动实现基于[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/字符设备驱动框架/字符设备驱动框架\|字符设备驱动框架]], 字符设备驱动框架中提到的功能, 这里不再赘述
- 该子系统是依赖于`pinctrl`子系统的, 只有当`pinctrl`设置引脚为`gpio`模式, 才会用到`gpio`子系统的`API`

# 子系统组成
## gpio控制器驱动

关键结构体和函数:
- `gpiochip_add_data()`: 注册`gpio`


主要包括下述工作:
1. 

驱动实例参考:
- **ST**: 集成到了`pinctrl`的驱动, 在`probe`中调用`gpiochip_add_data()`
	- 参考[[技术文档/Linux/Linux内核/源码结构/drivers/pinctrl/stm32/pinctrl-stm32.c\|pinctrl-stm32.c]]

# API
主要提供了一组函数, 用于配置`GPIO`

给使用`GPIO`子系统的设备驱动(即`GPIO`子系统的消费者)提供`API`, 具体的`API`参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h\|技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h]], 常见的有:
- `devm_fwnode_get_index_gpiod_from_child`: 获取`gpio_desc`
	- 使用`fwnode`抽象层
- `devm_gpiod_get`: 获取`gpio_desc`
- `...`
## 获取GPIO描述符
- `gpiod_get()`
- `devm_gpiod_get()`
- `devm_fwnode_get_gpiod_from_child()`
	- 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/gpio/consumer.h#devm_fwnode_get_gpiod_from_child()\|devm_fwnode_get_gpiod_from_child()]]
- `devm_fwnode_get_index_gpiod_from_child()`
- `devm_gpiod_get_index()`

# GPIO 属性相关
- `gpiod_is_active_low()`: 判断`gpio`是否为低电平有效
	- 电平有效性, 一般在设备树中定义

## GPIO防抖相关
- `gpiod_set_debounce()`: 设置`gpio`防抖时间, 单位微妙

## GPIO中断相关
- `gpiod_to_irq()`: 获取中断号

## GPIO状态相关
- `gpio_get_value()`: 直接获取`gpio`的状态值
- `gpio_set_value()`

## 申请GPIO管脚
- `gpiod_request`
- `gpio_request`
## 释放GPIO管脚
- `gpio_free`
## 设置GPIO输入模式
- `gpio_direction_input`
## 设置GPIO输出模式
- `gpio_direction_output`
	- `1`为高电平

# 消费者
# 设备树
## 定义
参考[[技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/gpio/gpio.txt\|gpio.txt]]

**实例**
```devicetree
```
## 引用
参考[[技术文档/Linux/Linux内核/源码结构/Documentation/devicetree/bindings/gpio/gpio.txt\|gpio.txt]]

**实例**
```devicetree
gpio-keys {
	compatible = "gpio-keys";
	autorepeat;
	key0: key0 {
		label = "USER-KEY0";
		linux,code = <114>;
		gpios = <&gpiog 3 GPIO_ACTIVE_LOW>; // 主要通过这个属性引用gpio
		gpio-key,wakeup;
	};
};
```




