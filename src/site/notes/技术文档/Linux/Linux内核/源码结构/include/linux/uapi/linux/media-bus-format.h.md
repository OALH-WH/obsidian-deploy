---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/源码结构/include/linux/uapi/linux/media-bus-format.h/","dg-note-properties":{}}
---

# MEDIA_BUS_FMT_FIXED宏

示例
```c
// 表示1个像素点使用3*8-bits表示
#define MEDIA_BUS_FMT_BGR888_3X8 0x101b

// BE表示高位先传输, LE表示低位传输
#define MEDIA_BUS_FMT_RGB888_2X12_BE 0x100b
```