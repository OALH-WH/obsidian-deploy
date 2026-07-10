---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/sonic-mgmt-common/translib architecture/translib_utils/","dg-note-properties":{}}
---

1. 常用API

1. needQuery

1. 判断当前节点是否是目标节点的父节点，子节点or兄弟姐妹节点

1. constructCountersTableKey

1. args

1. parentKey：初始key值

1. suffix：指定后缀

1. lastkey：末尾要添加的key值（一个rediskey由table 分隔符 key1 分隔符 key2...组成）

1. func

1. 把suffix和最后一个key通过‘_’ join

1. lastkey作为最后一个key