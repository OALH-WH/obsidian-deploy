---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/电层/oca层/","dg-note-properties":{}}
---

1. oca_am_data.c：oca层告警模块

1. 定义了注册告警处理函数的注册函数

1. oca_agent.c:

1. 调用了注册告警的函数来注册告警处理函数

1. alarmPluggableProc函数：判断是否上报模块告警

1. oca_am.c:oca层告警模块

1. 提供告警上报函数：alarm_report

1. 提供告警处理函数调用