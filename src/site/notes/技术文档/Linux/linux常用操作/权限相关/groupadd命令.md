---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/权限相关/groupadd命令/","dg-note-properties":{}}
---

# 作用
向系统添加一个组

# 配置
## 组信息
`/etc/group`: 存放所有组的信息
### 基本格式
用户组名称 : 用户组密码 : GID : 此用户组包含的账号名称

**字段**


# 基本格式
`groupadd [OPTIONS] <GROUP NAME>`

**可选参数**
- `-g`: 指定要创建的组的`GID`
- 

# 实例
```shell
groupadd -g 1000 kali
```