---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/OCM层/OCM常见API/","dg-note-properties":{}}
---

1. 实际API调用的注册好的API

1. 注册位置：各个表文件中定义注册，例如，sCurrentAlarmTable.c

1. MibQBC：筛选MIB数据

1. Mib_Set_Partial:设置一条数据的部分字段

1. MIB_REGISTER_CALLBACK:注册回调

1. 参数

1. 最后一个参数flag是用来判断是哪个字段发生变化的时候调用回调