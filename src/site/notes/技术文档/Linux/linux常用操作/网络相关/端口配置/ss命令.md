---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/端口配置/ss命令/","dg-note-properties":{}}
---

# 背景
- socket statistics，socket统计
- `netstat`命令的上位替代
# 依赖
# 安装
# 参数
- `-t`：只显示tcp socket
- `-u`：只显示udp socket
- `-l`：显示监听套接字
- `-n`：不解析为服务名
- `-p`: 显示进程标识符和程序名称
# 实例
## 查看指定端口状态
- `ss -tulnp | grep <port>`