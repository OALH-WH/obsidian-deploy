---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/二进制程序相关/nm命令/","dg-note-properties":{}}
---

# 背景
- [[技术文档/Linux/linux常用操作/二进制程序相关/符号表\|符号表]]
# 作用
- 显示文件的符号表
# 基本格式
- `nm <executable program>`
## 参数
- `-C, --demangle[=STYLE]`
	- 解码低级符号为用户符号
	- 可指定style, 可以为auto(default), gnu, lucid, arm... 