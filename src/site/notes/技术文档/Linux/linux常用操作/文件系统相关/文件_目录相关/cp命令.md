---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文件系统相关/文件_目录相关/cp命令/","dg-note-properties":{}}
---

# 背景
# 注意
## 行为分析
- 源目录 without / -> 目标不存在
	- 复制目录内容, 并创建目标目录
- 源目录 with / -> 目标不存在
	- 复制目录, 但会重命名为目标
- 源目录 without / -> 目标存在
	- 把目录复制到目标内部
- 源目录 with / -> 目标存在
	- 把目录内容复制到目标内部
# 基本格式
`cp [OPTIONS] SOURCE DEST`

**可选参数**
- `-p`: 等同于`--preserve=mode,ownership,timestamps`
- `--preserve[=ATTR_LIST]`: 保护文件复制时指定的属性不变
