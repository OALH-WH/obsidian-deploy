---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/网元常见操作/手动测试Linux板卡上能否正常访问客户侧模块/","dg-note-properties":{}}
---

1. 步骤

1. 首先看这个卡是通过什么访问模块的(通过硬件架构图来看)，一般是I2C，但可能是CPLD转I2C，或者FPGA转I2C等等

1. 查看I2C端口基地址，eg.product -q c 12,查看CPLD转I2C基地址,一个读地址，一个写地址

1. redmine上找硬件相关文档

1. product