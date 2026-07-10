---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C/Linux系统C接口/Linux系统C函数接口/","dg-note-properties":{}}
---

1. System V IPC

1.  头文件

1. sys/sem.h

1. sys/msg.h

1. sys/shm.h

1. 消息队列

1. 信号量

1. 共享内存

1. 可变参数的实现

1. 底层原理

1. 函数参数是从右向左依次入栈的，通过，指定第一个固定参数，我们可以确定可变参数列表的边界，即第一个可变参数，通过指定每个可变参数的类型，就可以得到每个可变参数所占内存空间大小，即可以遍历所有的可变参数

1. 头文件：stdarg.h

1. 常用宏

1. va_list

1. va_start

1. va_arg

1. va_end

1. 实现流程，可变参数至少需要一个固定参数

1. 创建va_list变量

1. 使用va_start初始化变量，例如va_start(va_list b, arg1)

1. 使用va_arg获取参数列表中的每个参数，例如a = va_arg(va_list b, type)

1. 使用va_end清理参数列表内存

1. 环境变量类

1. 头文件：stdlib.h

1. getenv函数

1. 作用：获取环境变量的值

1. setenv

1. 作用：设置环境变量

1. 时间类

1. 头文件：time.h

1. time(time_t *)函数

1. 作用：用来获取当前的时间戳(从1970年1月1日0时)

1. 参数

1. arg1：用来存储时间戳的变量地址

1. 返回值:time_t

1. localtime(time_t *)函数

1. 作用：将time_t类型的时间戳转换为本地时间（本地时间根据所在时区和UTC时间进行调整后的时间）的struct tm结构

1. 返回值：一个全局struct tm类型的变量的指针

1. 注意：输出经过时区处理之后的时间之前，需要设置环境变量TZ='America/New_York'

1. strftime函数

1. 作用：将struct tm结构转换为自定义的字符串

1. gmtime函数

1. 作用：类似于localtime函数，但是返回的是UTC时间（不受地理位置的影响，不包含时区偏移）

1. 返回值：一个全局struct tm类型的变量的指针

1. clock_gettime(CLOCK_MONOTONIC, &ts)

1. 结构体

1. struct tmspec

1. 信号类

1. 

1. 线程类

1. 

1. 测试类(is,if等)

1. access(const char *pathname,int mode)

1. 头文件

1. unistd.h

1. 作用：测试用户是否具有某种访问权限

1. 参数

1. pathname：文件路径

1. mode：测试的模式

1. R_OK：是否具有读权限

1. W_OK：是否具有可写权限

1. X_OK：是否具有可执行权限

1. F_OK:文件是否存在

1. 返回值

1. 成功，return 0

1. 1

1. 锁类

1. 进程锁

1. fcntl(int fd,int cmd,...)

1. 头文件

1. unistd.h

1. fcntl.h

1. 作用：文件上锁、解锁等

1. 参数

1. fd: 文件描述符

1. cmd

1. F_GETLK,表示获取锁

1. F_SETLK,异步设置锁，即会直接返回

1. F_SETLKW,同步设置锁，即会阻塞

1. 文件锁的表示

1. struct flock

1. l_type

1. F_RDLCK: 设置读锁

1. F_WRLCK：设置写锁

1. F_UNLCK：设置解锁

1. l_whence

1. SEEK_SET：以文件开头为锁定的起始位置

1. SEEK_CUR：以目前文件读写位置为锁定的起始位置

1. SEEK_END：以文件结尾为锁定的起始位置

1. l_start：基于l_whence的偏移量

1. l_len：加锁的长度，0表示对整个文件加锁

1. l_pid：加锁进程的进程id

1. 字符串类

1. strtok

1. strtoul（const char* nptr, char** endptr,int base）

1. 作用：会扫描参数nptr字符串，跳过前面的空白字符，直到遇到数字或者正负号才开始做转换，遇到非数字或字符串结束时结束转换

1. 头文件：stdlib.h

1. 注意

1. base == 0：采用10进制转换，但是遇到'0x/0X'前置字符则会使用16进制转换，遇到'0'前置字符，则会使用8进制转换

1. 若endptr不为NULL，则会将遇到的不符合条件而终止的字符指针由endptr传回

1. 返回值

1. 若成功，返回转换后的整型

1. 若失败或者str为空字符串，返回0