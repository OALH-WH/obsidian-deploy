---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/sonic-mgmt-common/根据path订阅key/","dg-note-properties":{}}
---

1. translib.subscribe

1. translateSubscribe根据path获取要订阅的key

1. 第一个返回值不用管

1. 第二个存储了tb，key，dbNum等信息 //nInfo

1. err

1. 完善nInfo的信息, app, appInfo...

1. 把nInfo放入一个数组map中， map的key为dbNum

1. 如果path是alarm/state， 则多订阅一个hisevent表

1. sInfo中存储了queue

1. 调用startSubscribe

1. startSubscribe

1. 第一个参数：sInfo

1. 第二个参数：数组map dbNotificationMap

1. 遍历map，调用startDBSubscribe

1. startDBSubscribe

1. 第一个参数opt

1. 第二个参数[]notificationInfo

1. 遍历数组

1. 创建sKey

1. ts：tbname

1. key：key

1. 添加进sKeyList

1. nInfo存入nMap中， key为sKey

1. sInfo存入sMap中， key为nInfo

1. 遍历dbs，调用SubscribeDB

1. SubscribeDB

1. 