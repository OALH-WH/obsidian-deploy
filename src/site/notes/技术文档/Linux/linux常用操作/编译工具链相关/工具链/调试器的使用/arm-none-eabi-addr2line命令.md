---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/arm-none-eabi-addr2line命令/","dg-note-properties":{}}
---

# 示例
```shell
# 查看地址对应位置
arm-none-eabi-addr2line -e your_firmware.elf 0x08004dbf
```