---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/sonic-mgmt-rest/server/","dg-note-properties":{}}
---

1. handler.go

1. process：服务器主要线程

1. 获取请求body，传给TranslibArgs.data

1. 获取请求path, 传给TranslibArgs.path

1. 调用invokeTranslib

1. invokeTranslib:根据请求类型，调用translib来处理

1. getPathForTranslib:获取在translib中使用的path

1. 