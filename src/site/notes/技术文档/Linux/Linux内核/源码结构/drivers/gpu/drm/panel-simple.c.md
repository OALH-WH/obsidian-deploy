---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c/","dg-note-properties":{}}
---

# struct panel_desc
关于某个显示屏设备的描述

包括下述成员:
- `modes`: 指针, 指向这个屏幕支持的像素模式数组, 比如`RGB8888`
	- 参考[[技术文档/常见硬件模块/显示模块/基本知识#像素格式\|基本知识#像素格式]]
- `size`: 显示屏大小, 包括长, 宽两个成员, 单位都是毫米
	- `height`
	- `width`
- `bpc`: 每种颜色占用的`bit-size`
- `bus_format`: 参考[[技术文档/Linux/Linux内核/源码结构/include/linux/uapi/linux/media-bus-format.h#MEDIA_BUS_FMT_FIXED宏\|media-bus-format.h#MEDIA_BUS_FMT_FIXED宏]]
# struct panel_simple
用于管理显示屏设备的

包括下述成员:
- `desc`: 指针, 指向单/多个显示屏信息
	- 类型参考[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#struct panel_desc\|#struct panel_desc]]
- `no_hpd`: 

# panel_simple_platform_driver变量
使用平台驱动框架注册驱动, 和设备树设备节点匹配

包括下述实现:
- `probe`: [[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#panel_simple_platform_probe()\|#panel_simple_platform_probe()]]
# panel_simple_funcs变量

# platform_of_match变量
平台总线设备兼容表

是个数组, 成员类型参考[[技术文档/Linux/Linux内核/源码结构/include/linux/mod_devicetable.h#struct of_device_id\|mod_devicetable.h#struct of_device_id]]

# panel_simple_platform_probe()
注册到平台总线上的`probe`回调函数

包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#panel_simple_probe()\|#panel_simple_probe()]]


# panel_simple_probe()

包括下述工作:
1. 设置屏幕参数
2. 获取背光设备节点, **设备树需要提供backlight属性**
3. 初始化显示屏
	- 调用[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#drm_panel_init()\|#drm_panel_init()]]
4. 设置`panel->base.funcs`回调函数为[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#panel_simple_funcs变量\|#panel_simple_funcs变量]]

# panel_simple_init()
屏幕驱动初始化函数

包括下述工作:
1. 注册平台驱动
	1. 使用[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#panel_simple_platform_driver变量\|#panel_simple_platform_driver变量]]
2. 如果屏幕为`DSI`接口, 则注册`MIPI DSI`总线驱动