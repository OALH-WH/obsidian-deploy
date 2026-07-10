---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/valgrind命令/","dg-note-properties":{}}
---

1. 安装

1. sudo apt install valgrind

1. 常用参数

1. --track-origins //查看未定义/未初始化的变量的位置

1. --vgdb //开启gdb server

1. --vgdb-error //使用--vgdb-error=0,表示**只要出现任何错误就停住**，相当于断点

1. 常用操作

1. 检测所有内存泄漏//未释放的内存的完整堆栈信息，包括内存越界

1. valgrind --tool=memcheck --leak-check=full ./file

1. 检测到错误直接退出

1. valgrind --tool=memcheck --error-exitcode=1 ./file

1. 检测死锁