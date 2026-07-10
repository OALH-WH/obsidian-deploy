---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/背景/Linux设备号/","dg-note-properties":{}}
---

# 设备号的组成
- 为了方便管理，Linux 中每个设备都有一个设备号，设备号由主设备号和次设备号两部分 组成，主设备号表示某一个具体的驱动，次设备号表示使用这个驱动的各个设备
- 设备号的结构类型为`dev_t`, 其本质为`unsigned int`类型, 即32位数, 其中
	- 高12位: 主设备号, 可用宏`MAJOR(dev number)`得到
	- 低20位: 次设备号, 可用宏`MINOR(dev number)`得到
```cpp
# 定义在include/linux/types.h
typedef __u32 __kernel_dev_t;
typedef __kernel_dev_t dev_t;
```