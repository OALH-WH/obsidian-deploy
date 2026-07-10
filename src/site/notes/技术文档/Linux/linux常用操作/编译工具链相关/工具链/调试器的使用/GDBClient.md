---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/GDBClient/","dg-note-properties":{}}
---

# 背景
# 依赖
- 调试程序编译时携带参数 `-g`
# 安装
# 基本格式
# 参数
# 交互子命令
## list
- `list <file name>:<line number>`
- 用于列出某个源文件的代码, 并切换到该文件, 此时可使用`info source`命令
	- 一般情况下结果都是`No such file or directory`, 因为部署环境不会存在源文件
	- **没有找到文件不影响`info source`命令的使用**
- `eg. list main.c:1`
## target
-  `remote <host>:<port>`: 连接到远程调试服务器 
	- `eg. target remote localhost:1234`
## `help`
- 查看帮助信息, `eg. help info`
## `continue`
## `run`
- 开始运行指定的程序
## `kill`
- 杀死当前运行的程序
## `step`
- 单步调试, 会进入函数
## `next`
- 单步调试, 不会进入函数
## `set`
- `stop-on-solib-events 1/0`: 设置在每次加载动态库时暂停
- `architecture <ARCH>`: 切换解析程序用的架构
	- 可通过`set architecture + <Tab>`来查看支持哪些架构
## `break`
- 打断点
## `delete, d`
- 删除断点
## `info`
- `connections`: 查看和调试服务器的连接状态
- `sharedlibrary`: 查看已经加载的动态库
- `breakpoints`: 查看断点信息
- `threads`: 查看线程信息
- `source`: 查看当前正在执行的代码所在源文件信息, 包括路径...
{ #67adbe}

- `sources`: 查看所有依赖的源文件以及库 
- `files`: 查看所有段
## `thread`
- apply
	- `all bt`: 查看所有线程的调用栈
## `catch`: 捕获
- `syscal`: 捕获系统调用
	- 示例: `eg. `
# 实例
## 开发机加载调试程序, 远程调试目标板
- 步骤
	- 
## 打断点
- `break <func name>`: 函数上断点
- `break <file>:<line number>`: 行号上断点
## 删除断点
- `delete <point number>`: 删除断点, 断点序号可通过 `info breakpoints`查看
---
# 实例
## 查找某一个源文件的相关信息
### 步骤
- 
# 常见问题
## 调试器调试日志显示没有找到源文件
- 原因
	- 通常是因为是在其他机器上编译的, 运行机器上没有源文件
- 解决方法
- 示例
```shell
[Switching to Thread 0x7ff58c1070 (LWP 14432)]

Thread 5 "transceiver_cmd" hit Breakpoint 1, libappd::alarm_intr_thread_func () at ./src/alarm.cc:99
99      ./src/alarm.cc: No such file or directory.
```
---