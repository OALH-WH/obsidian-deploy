---
{"dg-publish":true,"permalink":"/技术文档/C_C++/C/标准库/glibc/unistd/","dg-note-properties":{}}
---

# 常用函数
## `int access(const char *pathname, int mode);`
- 测试文件权限
### 参数
- `pathname`: 文件路径
- `mode`
	- `F_OK`: 测试文件是否存在
	- `...`
### 返回值
- 成功返回0
## isatty(int fd)
- 判断文件描述符是否为终端
- 使用示例
	- `eg. isatty(fileno(stdout))`: 判断标准输出是否是终端(TTY)