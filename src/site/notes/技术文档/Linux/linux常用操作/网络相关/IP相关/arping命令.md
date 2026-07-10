---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/IP相关/arping命令/","dg-note-properties":{}}
---

# 作用
测试`arp`数据包

# 基本格式
`arping [OPTIONS] <host | ip | MAC | -B>`

**可选参数**
- `-i`: 指定网络接口, `eg. eth0`

# 实例
```shell
sudo arping -i eth2 192.168.0.1
```