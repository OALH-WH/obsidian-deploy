---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/fs.h/","dg-note-properties":{}}
---

# struct file

包括下述成员:
- `private_data`: 空指针, 用于存储私有数据
	- 一般用于`open`函数中填充私有数据, 在`read/write`中使用
# struct file_operations

包括下述成员:
- `owner`
- `open`
- `read`
- `write`
- `release`

# alloc_chrdev_region()
动态申请设备号

**参数**
- `dev`: [[技术文档/Linux/Linux内核/源码结构/include/linux/types.h#dev_t\|types.h#dev_t]]类型, 保存申请到的起始设备号, 其中包括主设备和起始次设备号
- `baseminor`: 次设备号起始地址, 可以从0开始
- `count`: 要申请的设备号数量
- `name`: 用于标识这个**主设备号区间**
	-  **`/proc/devices` 文件**：这是最直接的应用。当驱动成功加载后，你执行 `cat /proc/devices`，就能看到一行显示你指定的 `name` 和系统分配的主设备号。这为开发者和管理员提供了一个清晰、易读的设备列表[](https://developer.aliyun.com/article/343255)[](https://juejin.cn/post/7361023886853603382)。
	- **`sysfs` 文件系统**：设备名称会关联到 `/sys/class/` 等目录下的设备信息中[](https://developer.aliyun.com/article/343255)[](https://juejin.cn/post/7361023886853603382)。用户态的热插拔管理工具（如 **udev** 和 **mdev**）正是通过读取 `/sys` 下的这些信息来识别新硬件，并自动在 `/dev` 目录下创建相应的设备文件的[](https://developer.aliyun.com/article/343255)。
	- **内核字符设备链表**：内核会将这个名称和设备号范围记录在内部的字符设备链表（`chrdevs` 数组）中，用于设备号的管理和查找。


**实例**
1. `i2c`从设备批量申请设备号
	1. 在 I2C 框架中，`alloc_chrdev_region` 用于模块初始化时**提前预留**设备号池，然后在每个 I2C 设备 `probe` 时，通过 `ida_alloc` 动态分配一个空闲的次设备号，组合成最终设备号，再注册字符设备。这样既统一了主设备号，又支持了多个物理/逻辑设备实例，完美符合多设备场景

# unregister_chrdev_region()
释放动态申请到的设备号

**参数**
- `from`: 主设备号
- `count`: 次设备号数量, 应和**动态申请设备号**时指定的`count`一致

