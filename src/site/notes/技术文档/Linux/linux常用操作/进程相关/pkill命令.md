---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/进程相关/pkill命令/","dg-note-properties":{}}
---

# 作用
杀掉匹配到的进程
# 基本格式
`pkill <OPTIONS> <PATTERN>`


**可选参数**
- `-<signal>`: 指定发送的信号, `eg. -9`, 默认是`SIGTERM`, 所有信号参考[[技术文档/Linux/linux常用操作/IPC相关/信号相关/信号总览\|信号总览]]