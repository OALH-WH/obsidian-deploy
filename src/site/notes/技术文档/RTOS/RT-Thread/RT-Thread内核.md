---
{"dg-publish":true,"permalink":"/技术文档/RTOS/RT-Thread/RT-Thread内核/","dg-note-properties":{}}
---

# RT-Thread 启动流程
1. `startup_xx.S`: 启动文件
	- `mdk`
	- `iar`
	- `gcc`
2. `rtthread_startup`
3. `rt_hw_interrupt_disable`: 关闭硬件中断
4. `rt_hw_board_init`: 板载资源初始化
{ #031d5e}

	1. `rt_components_board_init`: RT组件初始化
		-  `board init functions`: 按降序从高优先级开始排序
			1. `init board`
			2. `init prev`
			3. `...`
5. `...`
6. `main`
## 参考
![Pasted image 20260325131658.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/RTOS/RT-Thread/resources/Pasted%20image%2020260325131658.png)
# RT-Thread内存分布
- `Code`: 代码段, 一般占用`Flash`空间
- `RO-data`: 存放程序中定义的常量, 一般占用`Flash`空间
- `RW-data`: 存放程序中初始化为非0值的全局变量, 一般占用`RAM`空间
- `ZI-data`: 存放未初始化的全局变量和初始化为0的变量, 一般占用`RAM`空间
## 可执行映像文件
- 包括`Code`, `RO-data`, `RW-data`段, 其中`RW-data`段会在启动代码执行时被`copy`到`RAM`中
- 而`ZI-data`段因为全是0, 不会占用映像文件大小, 而是直接在启动代码执行时, 在`RAM`中创建并初始化为`0`, 因此未初始化的全局变量最后的默认值是`0`
# RT-Thread 自动初始化机制
- 其自动初始化的时机, 参考[[技术文档/RTOS/RT-Thread/RT-Thread内核#^031d5e\|board init functions]]

|**初始化顺序**|**宏接口**|**描述**|
|---|---|---|
|1|INIT_BOARD_EXPORT(fn)|非常早期的初始化，此时调度器还未启动|
|2|INIT_PREV_EXPORT(fn)|主要是用于纯软件的初始化、没有太多依赖的函数|
|3|INIT_DEVICE_EXPORT(fn)|外设驱动初始化相关，比如网卡设备|
|4|INIT_COMPONENT_EXPORT(fn)|组件初始化，比如文件系统或者 LWIP|
|5|INIT_ENV_EXPORT(fn)|系统环境初始化，比如挂载文件系统|
|6|INIT_APP_EXPORT(fn)|应用初始化，比如 GUI 应用|
