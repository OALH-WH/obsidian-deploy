---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/搜索相关/lsof命令/","dg-note-properties":{}}
---

# 背景
- 列出所有打开的文件, 包括网络套接字
- 性能相对较慢, 因为要遍历所有打开的文件
# 基本格式
- `lsof <file path>`: 查看指定文件被哪些进程访问
# 参数
- `-i [FILTE RULE]`: 列出打开的网络套接字
- `-c <CMD NAME>`: 查看指定进程名打开的文件
- `-p <PID>`: 查看指定进程打开的所有文件
- `-P`: 大写, 禁止端口到服务名的转化
# 内容解析
## 列
- `COMMAND`: 进程名
- `PID`: 进程ID
- `USER`: 用户名
- `FD`: ???
- `TYPE`: 文件类型
	- `IPv4`
	- `FIFO`
	- `IPv6`
	- `...`
- `DEVICE`: ???
- `NODE`: ???
- `NAME`: ???
# 实例
## 查看所有玩了个套接字
- `sudo lsof -i`
## 查看使用了22端口的套接字
- `sudo lsof -i :22`