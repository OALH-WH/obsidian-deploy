---
{"dg-publish":true,"permalink":"/技术文档/Linux/Shell/bash/","dg-note-properties":{}}
---

# 配置文件
## ~/.bashrc
## 常见配置
- 
# Bash扩展语法
## **
- 表示递归匹配
- 需要开启`globstar`, 参考[[技术文档/Linux/linux常用操作/Shell配置相关/shopt命令#开启bash的globstar\|shopt命令#开启bash的globstar]]
---
1. 实例

2. 绑定ctrl+o到某个操作

3. 步骤

4. .bashrc中添加如下

5. bind -x '"\C-o":__fzf_launcher' #__fzf_launcher为shell函数