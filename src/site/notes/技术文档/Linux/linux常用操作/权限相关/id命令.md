---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/权限相关/id命令/","dg-note-properties":{}}
---

# 背景
显示指定用户的`UID GID`, 以及`groups`
不指定用户, 默认显示当前`shell`进程的有效用户的相关信息
# 基本格式
```shell
id <options> [USER]
```
**可选参数**
- `-u`: 显示当前`shell`进程的有效用户`UID`
	- `eg. id -u`