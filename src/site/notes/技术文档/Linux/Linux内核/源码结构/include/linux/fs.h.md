---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/fs.h/","dg-note-properties":{}}
---

# 函数
## 动态申请设备号
### `int alloc_chrdev_region(dev_t *dev, unsigned baseminor, unsigned count, const char *name)`
#### 参数
- `dev`: 保存申请到的设备号, 其中包括主设备和起始次设备号
- `baseminor`: 次设备号起始地址, 可以从0开始
- `count`: 要申请的设备号数量
- `name`: 设备名称
## 释放动态申请到的设备号
### `void unregister_chrdev_region(dev_t from, unsigned count)`
#### 参数
- `from`: 主设备号
- `count`: 次设备号数量, 应和**动态申请设备号**时指定的`count`一致