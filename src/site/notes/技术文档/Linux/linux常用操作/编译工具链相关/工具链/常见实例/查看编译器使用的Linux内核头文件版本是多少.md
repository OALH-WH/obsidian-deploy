---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/常见实例/查看编译器使用的Linux内核头文件版本是多少/","dg-note-properties":{}}
---

# 方式1: 检索版本头文件
# 步骤
## 搜索工具链目录下 `version.h`文件
- 找到此文件中定义的类似于下述信息
- 反推出Linux内核版本
```cpp
#define LINUX_VERSION_CODE 267277
#define KERNEL_VERSION(a,b,c) (((a) << 16) + ((b) << 8) + (c))

// Linux version is 4.20.13
```