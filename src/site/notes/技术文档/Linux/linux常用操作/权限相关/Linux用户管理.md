---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/权限相关/Linux用户管理/","dg-note-properties":{}}
---

# 常见命令
## `su`
- 切换用户重新登陆
- 示例
	- `eg. sudo su`: 切换到root用户
	- `eg. su - $USER`: 重新登陆当前用户
## `login`
---
1. 用户管理

2. 实例

3. 查看用户密码

4. 

5. 权限管理

6. 实例

7. 设置setgid

8. 方式

9. chmod g+s <file | directory>

10. 作用

11. for file： 让普通用户以特定组的权限执行程序

12. for directory：确保所有创建的文件都属于同一个组

13. 识别

14. ls -l

15. file：-rwxr-sr-x

16. directory：drwxr-sr-x

17. 添加用户

18. useradd

19. 设置密码

20. password

21. 删除用户

22. userdel

23. 查看用户

24. id

25. 切换用户

26. su

27. 用户组

28. 命令

29. chown:设置文件所有者和文件关联组的命令

30. -R:递归的更改文件夹和文件的所有人

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/linux%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C/images/WEBRESOURCE6ccad73a786067b2f6593d5bcfeffdf6image.png)

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/linux%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C/images/WEBRESOURCE3d8bbc570e6f02b67e015c2bb4a536ddimage.png)

```text
/etc/passwd
账号名称 : 密码 : UID : GID : 用户信息说明列 : 主文件夹 : shell

root : x : 0 : 0 : root : /root : /bin/bash
```

```text
/etc/shadow
账号名称 : 密码 : 最近改动密码的日期 : 密码不可被改变的天数 : 密码需要重新更改的天数 : 更改提醒天数 : 密码过期后账号的宽限时间 : 账号失效日期 : 保留

root : (字符串，此处打码) : 200 : 0 : 99999 : 7 : : :
```

```text

/etc/group
用户组名称 : 用户组密码 : GID : 此用户组包含的账号名称

root : x : 0 : root
```

```text
/etc/gshadow
用户组名 : 密码 : 用户组管理员账号 : 该用户组包含的账号名称

root : : : root
```