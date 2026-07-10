---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C/标准库/glibc/stdio/","dg-note-properties":{}}
---

# 文件内容获取相关
## `char *fgets(char *s, int size, FILE *stream);`
### 参数
### 返回值
# 执行shell命令相关
## `FILE *popen(const char *command, const char *type);`
- 用于创建一个管道，启动一个子进程执行指定的 shell 命令，并返回一个文件指针
### 参数
- `command`: 要执行的shell命令
- `type`: 管道的方向
### 返回值
- 成功返回`FILE *`
- 失败返回`NULL`
## `int pclose(FILE *stream);`
- 和`popen()`函数配套使用, 关闭管道并获取命令执行结果状态