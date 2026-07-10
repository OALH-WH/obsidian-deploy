---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/IP相关/networking网络管理/","dg-note-properties":{}}
---

1. 配置文件路径

1. /etc/network/interfaces

1. 实例

1. 配置静态ip

```
auto eth0
iface eth0 inet static
    address 192.168.1.100  # 静态IP地址
    netmask 255.255.255.0  # 子网掩码
    gateway 192.168.1.1    # 默认网关
    dns-nameservers 8.8.8.8 8.8.4.4  # DNS服务器
```

1. 服务

1. networking