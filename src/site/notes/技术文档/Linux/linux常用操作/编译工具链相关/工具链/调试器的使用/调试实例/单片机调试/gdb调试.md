---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/调试实例/单片机调试/gdb调试/","dg-note-properties":{}}
---

1. 注意

1. 单片机调试是通过gdbserver和gdb client一起调试的

1. gdbserver负责和调试器通信, gdb client和gdbserver通信, 调试器负责和目标开发板通信

1. 常见的有openOCD, ST-gdbserver, J-Link gdbserver

1. gdb client使用