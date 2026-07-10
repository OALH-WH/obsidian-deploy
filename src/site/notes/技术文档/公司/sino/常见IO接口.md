---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/常见IO接口/","dg-note-properties":{}}
---

1. 读写CPLD寄存器

1. product -c -r reg

1. 读写FPGA寄存器

1. product -f -r reg

1. 读写I2C扩展FPGA寄存器

1. product -b 端口 fpga地址 -r reg

1. 读写FPGA扩展MDIO寄存器

1. prodcut -y 端口 1 -r reg