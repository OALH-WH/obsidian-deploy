---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/进程相关/exec命令/","dg-note-properties":{}}
---

# 作用
以将要执行的程序/命令替换为当前进程, 原来的程序直接删除
不加`exec`执行程序/命令, 就是创建一个子进程执行