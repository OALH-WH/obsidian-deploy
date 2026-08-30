---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/device.h/","dg-note-properties":{}}
---

# 总线结构体
`struct bus_type {...};`
# struct device_driver
设备驱动类, 包括下述成员:
- `name`: 驱动名称(**必须定义**)
- `owner`: (**可选**)
- `of_match_table`: 定义兼容的设备列表(**必须定义**)

# struct device
设备类, 包括下述成员:
- `parent`: 表示父设备
- `driver`: 分配给这个设备的驱动, 类型为[[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#struct device_driver\|#struct device_driver]]
- `of_node`:  设备树节点指针
- `platform_data`: `void *`类型的指针变量, 设备树普及之前, 老版内核用于传递设备相关硬件参数到驱动的成员
{ #f95f04}

	- 一般在定义设备结构体变量时赋值, 比如
```c
/* 注册 platform_device 时挂上去 */
static struct platform_device my_key_device = {
    .name = "gpio-keys",
    .id   = -1,
    .dev  = {
        .platform_data = &my_key_pdata,  /* ← 在这里赋值 */
    },
};
```
- 

# devm_kzalloc()
作用同`kzalloc`一致, 清零初始化, 分配堆空间, 但这块内存和设备实例绑定, 不用手动释放

**参数**
- `gfp`: 分配标志
	- `GFP_KERNEL`: 常用
**返回值**

# devres_alloc()
用于实现设备资源的自动管理, 配合`devres_add`和`devres_free`使用

**参数**
- **`release`**：这是一个回调函数，定义了当设备被移除或驱动卸载时，应如何清理和释放该特定类型的资源（例如，`iounmap` 用于释放IO内存映射）。
- **`size`**：你需要为该资源的私有数据存储申请多大的内存空间[](https://git.zx2c4.com/linux/commit/drivers/base/devres.c?id=d3e6975e0f25044c4c86f5a42c9917090973636b)[](https://www.e-com-net.com/article/1746397880601559040.htm)。常见做法是让这个私有数据包含资源本身（如 `dma_addr_t`）或其指针。
- **`gfp`**：这是标准的内存分配标志（如 `GFP_KERNEL`），告诉内核在何种上下文中分配内存。

# devres_add()
和设备节点绑定, 在设备卸载时自动调用使用`devres_alloc`时指定的`release`回调
# devres_free()
当没有达到调用`devres_add`函数的条件时, 要调用`devres_free`来释放空间



# class_create()
创建抽象设备类

**参数**
- `owner`: 一般为`THIS_MODULE`
- `name`: 抽象类名, 会映射到系统的`/sys/class`目录下


# device_create()


# dev_get_platdata()
用于获取[[技术文档/Linux/Linux内核/源码结构/include/linux/device.h#^f95f04\|#^f95f04]]成员变量

包括下述工作:


# dev_name()
获取设备名称

**来源**
- **驱动代码显式设置**：在注册设备前，通过 `dev_set_name(&pdev->dev, "my_uart")` 手动赋名。
- **设备树（DTS）的映射**：对于平台设备（Platform Device），内核在解析设备树时，会默认将 `dts` 节点名（或节点名@地址）作为设备名。例如，如果你的 DTS 节点是 `uart@4000d000`，`dev_name()` 通常返回 `"uart"` 或 `"4000d000.uart"`（取决于总线匹配）。
- **传统板级代码**：在旧式非设备树启动中，是注册 `platform_device` 时传入的 `.name` 字段。

# dev_set_name()
显式设置设备名称