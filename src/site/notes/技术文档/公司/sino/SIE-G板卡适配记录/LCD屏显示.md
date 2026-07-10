---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SIE-G板卡适配记录/LCD屏显示/","dg-note-properties":{}}
---

1. polling_data //如果有LCD屏

1. 判断机框类型，如果是SHELF_A || d2u_release_shelf

1. 判断是否按下按钮，如果是

1. 清除寄存器记录

1. 更新lcd_timer为当前时间

1. 触发按钮事件

1. 否则

1. 判断按钮状态，如果是ON || UPDATE

1. 如果记录的亮光开始时间在当前时间之后，更新lcd_timer为当前时间 //card_info.lcd_timer记录的亮光开始时间

1. 在60s内没有任何按下的行为事件，自动关闭LCD背光

1. 改按钮状态为update

1. 触发事件

1. 否则 //没有此逻辑

1. 否则 //没有此逻辑

1. siec trigger lcd event //根据当前按钮状态触发事件，事件类型会发送到ocm层 // ocm cfp app lcd.c

1. init状态

1. 事件：初始化事件

1. 设置下一个lcd按钮状态：off

1. off状态

1. 事件：打开lcd背光事件,on

1. 设置下一个lcd按钮的状态：on

1. on状态

1. 事件：更新事件,update

1. 设置下一个lcd按钮的状态：update

1. update状态

1. 事件：关闭背光事件,off

1. 设置下一个lcd按钮的状态：off