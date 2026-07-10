---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/dd命令/","dg-note-properties":{}}
---

# 基本格式
**位置参数**
- `if=<file path>`
- `of=<file path>`: 文件可不存在
- `bs=<size>`: 一次写入多大的数据
	- `1M`: 1MB
	- `...`
- `count`: 写入次数
- `oflag`: 写入模式
	- `append`: 追加写入
- `conv`:
	- `notrunc`: 确保文件不会被截断, 一般和`oflag=append`一起使用
	- 
	- 
# 可选参数
# 实例
## 创建一个空文件, 并指定大小
- `eg. dd if=/dev/zero of=/.../test.txt bs=1M count=1000`