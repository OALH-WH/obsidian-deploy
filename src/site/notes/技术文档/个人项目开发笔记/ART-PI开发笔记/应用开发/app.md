---
{"dg-publish":true,"permalink":"/技术文档/个人项目开发笔记/ART-PI开发笔记/应用开发/app/","dg-note-properties":{}}
---

# 功能
## 兼容bootloader设计
## flash分区设计
预计使用`fatfs`, 分区划分如下:

| sector       | start addr    | size    |
| ------------ | ------------- | ------- |
| `bootloader` | `0x0800 0000` | `128KB` |
| `APP`        |               |         |


