---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/leds/leds-gpio.c/","dg-note-properties":{}}
---


# gpio_leds_create()

包括下述工作:
1. 定义必要的变量
	- `dev`: 指针, 指向驱动匹配到的设备节点, 即`leds`
	- `child`: 指针, 用于遍历`leds`节点的子节点
	- `priv`: 指针, 用于统一管理`leds`子节点
2. 遍历`leds`的子节点
	1. 定义必要的变量
		- `led_dat`: 表示单个`led`的节点信息
		- `led`
	2. 获取节点相关属性
	3. 创建`led`设备, 进行相关配置
		- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/leds/leds-gpio.c#create_gpio_led()\|#create_gpio_led()]]函数

# create_gpio_led()
包括下述工作:
1. 










---
# leds-gpio.c 设备树资源获取分析文档

## 概述

`drivers/leds/leds-gpio.c` 是一个 GPIO LED 驱动，通过设备树（Device Tree）或传统平台数据（board files）来获取硬件资源。本文档聚焦于**设备树路径**，完整梳理其资源获取流程。

---

## 1. 驱动与设备树的匹配

```c
static const struct of_device_id of_gpio_leds_match[] = {
    { .compatible = "gpio-leds", },
    {},
};
MODULE_DEVICE_TABLE(of, of_gpio_leds_match);
```

- 设备树节点必须包含 `compatible = "gpio-leds";`
- 驱动通过 `of_match_table` 注册，内核在设备树解析时匹配到此驱动，调用 `probe`

---

## 2. Probe 入口：`gpio_led_probe()`

```c
static int gpio_led_probe(struct platform_device *pdev)
```

两种路径：

|路径|条件|处理函数|
|---|---|---|
|传统平台数据|`pdata && pdata->num_leds`|内联循环 + `gpio_led_get_gpiod()`|
|**设备树/ACPI**|否则|`gpio_leds_create(pdev)` ← 重点|

设备树路径走 `gpio_leds_create()`。

---

## 3. 核心函数：`gpio_leds_create()` — 从 DT 获取资源的完整流程

```c
static struct gpio_leds_priv *gpio_leds_create(struct platform_device *pdev)
```

### 3.1 获取子节点数量

```c
count = device_get_child_node_count(dev);
if (!count)
    return ERR_PTR(-ENODEV);
```

- 遍历设备树节点下的所有子节点（每个子节点代表一个 LED）
- 如果没有子节点，返回 `-ENODEV`

### 3.2 分配私有数据结构

```c
priv = devm_kzalloc(dev, sizeof_gpio_leds_priv(count), GFP_KERNEL);
```

- 使用 `devm_` 系列（device-managed），自动释放，无需手动 free

### 3.3 遍历每个子节点

```c
device_for_each_child_node(dev, child) {
```

对应设备树结构：

```dts
gpio-leds {
    compatible = "gpio-leds";
    led0 {
        gpios = <&gpio1 0 GPIO_ACTIVE_LOW>;
        ...
    };
    led1 {
        gpios = <&gpio1 1 GPIO_ACTIVE_HIGH>;
        ...
    };
};
```

`device_for_each_child_node` 宏展开为（定义在 `include/linux/property.h`）：

```c
for (child = device_get_next_child_node(dev, NULL); child;
     child = device_get_next_child_node(dev, child))
```

### 3.4 获取 GPIO 资源 — 最关键的步骤

```c
led.gpiod = devm_fwnode_get_gpiod_from_child(dev, NULL, child,
                                             GPIOD_ASIS, NULL);
```

**函数调用链：**

```
devm_fwnode_get_gpiod_from_child()
    → devm_fwnode_get_index_gpiod_from_child(dev, con_id=NULL, index=0, child, ...)
        → 遍历 gpio_suffixes[] = {"gpios", "gpio"} 构造属性名
        → fwnode_get_named_gpiod(child, "gpios", 0, ...)
            → 解析 child 节点的 "gpios" 属性
            → 返回 struct gpio_desc *
```

**参数说明：**

|参数|值|含义|
|---|---|---|
|`dev`|parent device|用于 devres 生命周期管理|
|`con_id`|`NULL`|无连接 ID，默认查找 `gpios` 属性|
|`child`|子节点 fwnode|要解析的设备树子节点|
|`flags`|`GPIOD_ASIS`|不配置 GPIO 方向/电平（后续手动配置）|
|`label`|`NULL`|标签先不设置，注册 LED 后再更新|

**对应 DT 属性：** `gpios = <&phandle gpio_num flags>;`

### 3.5 读取字符串属性

|DT 属性|读取方式|目标字段|说明|
|---|---|---|---|
|`linux,default-trigger`|`fwnode_property_read_string()`|`led.default_trigger`|触发模式，如 `"heartbeat"`|
|`default-state`|`fwnode_property_read_string()`|`led.default_state`|初始状态: `"on"` `"off"` `"keep"`|

```c
fwnode_property_read_string(child, "linux,default-trigger",
                            &led.default_trigger);

if (!fwnode_property_read_string(child, "default-state", &state)) {
    if (!strcmp(state, "keep"))
        led.default_state = LEDS_GPIO_DEFSTATE_KEEP;
    else if (!strcmp(state, "on"))
        led.default_state = LEDS_GPIO_DEFSTATE_ON;
    else
        led.default_state = LEDS_GPIO_DEFSTATE_OFF;
}
```

### 3.6 读取布尔属性（是否存在判断）

|DT 属性|读取方式|目标字段|
|---|---|---|
|`retain-state-suspended`|`fwnode_property_present()`|`led.retain_state_suspended`|
|`retain-state-shutdown`|`fwnode_property_present()`|`led.retain_state_shutdown`|
|`panic-indicator`|`fwnode_property_present()`|`led.panic_indicator`|

```c
if (fwnode_property_present(child, "retain-state-suspended"))
    led.retain_state_suspended = 1;
if (fwnode_property_present(child, "retain-state-shutdown"))
    led.retain_state_shutdown = 1;
if (fwnode_property_present(child, "panic-indicator"))
    led.panic_indicator = 1;
```

### 3.7 注册 LED 设备

```c
ret = create_gpio_led(&led, led_dat, dev, child, NULL);
```

`create_gpio_led()` 内部通过以下方式注册：

```c
if (template->name) {
    led_dat->cdev.name = template->name;
    ret = devm_led_classdev_register(parent, &led_dat->cdev);
} else {
    init_data.fwnode = fwnode;
    ret = devm_led_classdev_register_ext(parent, &led_dat->cdev, &init_data);
}
```

- 如果 `template->name` 被设置（来自 platform data），使用旧 API
- 否则（设备树路径），使用 `devm_led_classdev_register_ext()`，由内核从 fwnode 中的 `function` 和 `color` 属性自动生成名称

### 3.8 更新 GPIO consumer label

```c
gpiod_set_consumer_name(led_dat->gpiod, led_dat->cdev.dev->kobj.name);
```

- 等 LED class 注册完成、最终名称已知后，更新 GPIO consumer 的标签
- 方便 debug：`/sys/kernel/debug/gpio` 中可以看到每个 GPIO 被哪个 LED 占用

---

## 4. 完整设备树属性与 API 对照表

|DT 属性|类型|API|对应 struct gpio_led 字段|
|---|---|---|---|
|`gpios`|phandle+args|`devm_fwnode_get_gpiod_from_child()`|`gpiod`|
|`linux,default-trigger`|string|`fwnode_property_read_string()`|`default_trigger`|
|`default-state`|string|`fwnode_property_read_string()`|`default_state`|
|`retain-state-suspended`|boolean|`fwnode_property_present()`|`retain_state_suspended`|
|`retain-state-shutdown`|boolean|`fwnode_property_present()`|`retain_state_shutdown`|
|`panic-indicator`|boolean|`fwnode_property_present()`|`panic_indicator`|
|`function` / `color`|string|内核框架自动读取|LED 名称（自动生成）|

---

## 5. `fwnode_*` API 系列说明

该驱动统一使用 **fwnode**（firmware node）API 而非旧的 `of_*`（device tree specific）API。

**优势：** fwnode 是抽象层，同时支持：

- **设备树（DT）** — 通过 `of_fwnode_ops`
- **ACPI** — 通过 `acpi_fwnode_ops`

这样同一个驱动可以无需修改就同时支持设备树和 ACPI 平台。

核心 API 文件：

- `include/linux/property.h` — `device_for_each_child_node()`、`fwnode_property_read_string()`、`fwnode_property_present()`
- `include/linux/gpio/consumer.h` — `devm_fwnode_get_gpiod_from_child()`
- `drivers/gpio/gpiolib-devres.c` — 实际 GPIO 解析逻辑

---

## 6. 数据流总结

```
设备树节点 (compatible = "gpio-leds")
    │
    ├── of_match_table 匹配 → gpio_led_probe()
    │
    ├── gpio_leds_create()
    │       │
    │       ├── device_get_child_node_count()   ← 数子节点
    │       │
    │       ├── device_for_each_child_node()    ← 遍历每个子节点
    │       │       │
    │       │       ├── devm_fwnode_get_gpiod_from_child()  ← 获取 gpios
    │       │       ├── fwnode_property_read_string()       ← 读取字符串属性
    │       │       ├── fwnode_property_present()           ← 读取布尔属性
    │       │       └── create_gpio_led()                   ← 注册 LED
    │       │
    │       └── gpiod_set_consumer_name()       ← 更新标签
    │
    └── platform_set_drvdata()                  ← 保存私有数据
```

---

## 7. 参考文件

|文件|内容|
|---|---|
|`drivers/leds/leds-gpio.c`|本驱动|
|`include/linux/leds.h`|`struct gpio_led`、`struct gpio_led_platform_data`|
|`include/linux/property.h`|`device_for_each_child_node()`、fwnode 属性 API|
|`include/linux/gpio/consumer.h`|GPIO descriptor consumer API|
|`drivers/gpio/gpiolib-devres.c`|`devm_fwnode_get_index_gpiod_from_child()` 实现|
|`Documentation/devicetree/bindings/leds/leds-gpio.txt`|DT binding 文档|