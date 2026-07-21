---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/uaccess.h/","dg-note-properties":{}}
---


# copy_from_user()
把数据从内核空间拷贝到用户空间

包括下述工作:


**参数**
- `to`: 目标地址指针, 指向的是用户空间的内存缓冲区
- `from`: 源地址指针, 指向的是内核空间的内存缓冲区
- `n`: 要拷贝的数据长度, 以字节为单位
