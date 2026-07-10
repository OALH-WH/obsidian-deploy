---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/LED灯模块/","dg-note-properties":{}}
---

1. 顶层的封装函数set_local_led_by_local_alarm_result等被用来注册为告警处理函数

1. led的获取和配置主要在led_control.c文件里

1. 封装的几个函数

1. set_led_by_local_alarm_result: 在set_port_led这种封装函数的基础上根据告警类型来调用这些API做了封装，以提供给其他模块使用

1. ...

1. set_port_led：调用set_led，在set_led基础上根据led灯类型封装了一层

1. ...

1. set_led函数

1. 会到cdh层执行CDH_SetLedState函数

1. 再到sdd层执行SDD_SetLedState

1. oca_am_get_led_st函数：获取led灯的状态到mib

1. set_mib_arrary_led_st函数

1. 配置板卡led灯，如果配置的是port_start的类型，即8，则在8+port_num(1~8)-1的索引位置给定led灯状态

1. 其他则索引为端口号作为索引位给定led灯状态

1. led灯状态上传到mib表是通过ocm led.c文件

1. led灯配置的几个重要参数

1. led灯类型

1. led灯状态

1. led灯颜色