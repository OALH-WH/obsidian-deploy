---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文件系统相关/实例集/NFS服务器的实现/","dg-note-properties":{}}
---

# 背景
- 调用NFS系统接口, 最终会在内核创建一个RPC服务, 监听在2049端口, 等待客户端的请求