---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/进程相关/pgrep命令/","dg-note-properties":{}}
---

# 背景
打印类似使用`grep`匹配到的进程的`PID`
# 基本格式
**参数**

# 实例
## 批量杀掉匹配的进程
```shell
pgrep -f '/home/kali/.vscode-server' | xargs kill
```