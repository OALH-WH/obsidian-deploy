---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/权限相关/useradd命令/","dg-note-properties":{}}
---

# 作用
向系统中添加一个新的用户

# 基本格式
`useradd`

**可选参数**
- `-c`: 添加用户描述
- `-d`: 指定主目录路径, `eg. /home/kali`, 一般和`-m`一起使用, 否则不会创建主目录
- `-m`: 自动创建用户的主目录, `eg. /home/kali`
- `-s`: 指定登录`Shell`, `eg. zsh or bash...`
- `-u`: 手动指定UID
- `-g`: 指定初始主组
- `-G`: 将用户添加到附加组, 用逗号分隔

# 实例
```shell
useradd -s /bin/bash -u 1000 -g 1000 kali
```