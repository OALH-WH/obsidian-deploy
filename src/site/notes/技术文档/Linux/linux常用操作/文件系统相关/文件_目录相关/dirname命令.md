---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文件系统相关/文件_目录相关/dirname命令/","dg-note-properties":{}}
---

# 背景
# 作用
- 输出指定文件相对于 `$PWD`所在目录
# 注意
- 对不带路径的文件名返回.
- 对.返回., 因此不能用于查看当前目录的父级目录