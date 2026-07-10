---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/drivers/base/bus.c/","dg-note-properties":{}}
---

# bus_add_driver()
包括下述工作:
1. 调用[[技术文档/Linux/Linux内核/源码结构/drivers/base/dd.c#driver_attach()\|dd.c#driver_attach()]]函数


# bus_for_each_dev()
**参数**
- `fn`: 函数指针
包括下述工作:
1. 调用`fn`
