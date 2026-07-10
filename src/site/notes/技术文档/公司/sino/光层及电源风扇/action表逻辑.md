---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/光层及电源风扇/action表逻辑/","dg-note-properties":{}}
---

1. mib控制光层卡冷热起

1. ocm action.c

1. action类型为：ACTIONTYPE_WARMREBOOTCARD/COLDREBOOTCARD

1. 发送ipc消息到pca msg.c

1. pca msg.c

1. pca otn cfg recv handler函数接收对应action类型

1. 判断是否是d16he 1u /dci card/ d16hg dci card的卡

1. pca d16he set reboot reason to m4 card