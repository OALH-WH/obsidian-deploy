---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内核相关/sysctl命令/","dg-note-properties":{}}
---

# 配置
## 配置文件
- /etc/sysctl.conf
# 参数

- `-a`: 查看所有内核参数, 这里的内核参数包括运行时参数, 并非都是启动参数
- `-w`
# 实例
## 启用内核转发功能
### 命令(暂时)
- `sudo sysctl -w net.ipv4.ip_forward=1`
### 写配置文件(永久)
- `net.ipv4.ip_forward = 1`