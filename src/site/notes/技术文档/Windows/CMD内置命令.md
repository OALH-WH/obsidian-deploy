---
{"dg-publish":true,"permalink":"/技术文档/Windows/CMD内置命令/","dg-note-properties":{}}
---

# 其他
## net
- 管理网络环境、用户账户、服务、共享资源
### user
#### 基本格式
```shell
NET USER
[username [password | *] [options]] [/DOMAIN]
         username {password | *} /ADD [options] [/DOMAIN]
         username [/DELETE] [/DOMAIN]
         username [/TIMES:{times | ALL}]
         username [/ACTIVE: {YES | NO}]
```
#### 参数
- 
#### 实例
##### 修改用户密码
- `eg. net user sino *`
# 文本处理
## findstr
- 根据关键字筛选行
# 网络, 端口相关
## netstat
### 参数
- `/?`: 显示帮助信息
- `-n`: 不解析地址和端口显示,  可以加快程序执行速度
- `-a`: 显示所有连接和监听端口
- `-o`: 显示与每个连接关联的拥有进程PID
# 进程相关
## tasklist
- 查看进程
## taskkill
- 关闭指定进程
### 参数
- `/PID <PID>`: 终止指定进程
- `/F`: 强制终止进程