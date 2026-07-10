---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/驱动相关/drm驱动测试/modetest命令/","dg-note-properties":{}}
---

# 背景
用来测试驱动模型`drm`子系统, 是否正常工作
# 基本格式
``

**参数**
- `-M`: 指定`drm_driver`中定义的`name`, 并打印出`drm`子系统的相关信息
	- `name`: 比如`stm`厂商的`ltdc`驱动, 参考[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/stm/drv.c#drv_driver变量\|drv.c#drv_driver变量]]
- 
