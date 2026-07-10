---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/gdb命令/","dg-note-properties":{}}
---

# 基本格式
- `gdb --args <program> <program args>`
- `gdb <gdb args> <program>`
# 参数
- `--args`:  把参数还给被调试程序，而不是gdb
- `-p <PID>`: 把gdb附加到指定进程
- `-q`: 进入gdb交互界面
# 交互子命令
- 通用子命令参考[[技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/GDBClient\|GDBClient]]
---
# 常用实例

4. 检查死锁的位置

5. gdb -p <pid>

6. (gdb) thread apply all bt

7. 常用命令

8. 调试死锁, 打印每个线程的死锁位置

9. thread apply all bt

10. 连上例如valgrind启动的gdb server

11. target remote | vgdb

12. 一次性忽略信号SIGTRAP // 这个信号是valgrind，每次发现了未初始化值被使用就会插入一条SIGTRAP，把控制权给gdb

13. handle SIGTRAP pass nostop

14. 在程序调用了系统调用exit或者exit_group时处打断点 //release版也能用，不依赖符号表

15. catch syscall exit exit_group

16. 用gdb启动程序

17. gdb <cmd>

18. 运行程序

19. (gdb) run

20. 查看回溯信息

21. (gdb) backtrace

22. 继续执行, 直到遇到下一个断点

23. (gdb) continue