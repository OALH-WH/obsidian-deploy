---
{"dg-publish":true,"permalink":"/技术文档/AI/Agent/Open Code/opencode命令/","dg-note-properties":{}}
---

# 基本格式
- `opencode --port <PORT>`: 以当前目录为项目目录, 本地启动`opencode`, 并监听指定端口号
# opencode子命令
## server
- 开启支持远程访问的服务器
- `eg. opencode serve --port 1678`
## attach
- 临时连接到远程opencode服务, 永久可通过修改配置
- `eg. opencode attach http://172.17.1.57:1678`