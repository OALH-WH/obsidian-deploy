---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内核相关/getenforce命令/","dg-note-properties":{}}
---

# 背景
- 用来**查看 SELinux（Security-Enhanced Linux，安全增强型 Linux）当前的运行状态**。
# 配置
- `/etc/selinux/config`
# 命令输出及含义
在终端输入 `getenforce`，通常会有三种输出：

|输出|含义|
|---|---|
|**Enforcing**|**强制模式**。  <br>SELinux 正在运行，所有安全策略都会被执行。违反策略的操作会被阻止并记录日志。这是最安全、推荐的生产环境状态。|
|**Permissive**|**宽容模式**。  <br>SELinux 正在运行，但不会强制阻止任何操作。所有违反策略的操作只会被记录到日志中，而不会真的被拒绝。常用于调试或临时排查问题。|
|**Disabled**|**关闭模式**。  <br>SELinux 已完全关闭，既不强制执行也不记录任何安全策略。|
