---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/网络传输/ssh软件/","dg-note-properties":{}}
---

# 服务端
## 软件包
- `openssh-server`
## 配置
### `/etc/ssh/sshd_config`
`ssh`服务端配置
- `PermitRootLogin`
	 - yes：除了密钥, 还允许用密码登录
	- `prohibit-password`：只能密钥登录
- `PermitUserEnvironment`
	- `yes`: 使用`~/.ssh/environment`文件, 在登录`ssh`时加载里面定义的环境变量, `eg. MY_CUSTOM_VAR=hello`
- `StrictModes`: 设置`sshd`对配置文件的权限检查
	- `yes`: 打开权限检查
	- `no`: 关闭权限检查
### `~/.ssh/*`
- 目录没有可自己创建, 但目录和其中的文件所有者必须是和`~`一致...
- `authorized_keys`: 存储其他主机的公钥
	- 每个公钥占一行
	- 用于和其他主机密钥登陆, 即不用输入密码
## 包含的程序
### `sbin/sshd`
#### 基本格式

**参数**
- ``
### `ssh-keygen`
-  生成公私密钥
---
# 客户端
## 配置
### `<USER>/.ssh/config`: window
- 示例
```shell
Host 192.168.1.200(container)
    HostName 192.168.1.200
    User root
    Port 25000
    UserKnownHostsFile NUL # 不生成user know hosts file
    StrictHostKeyChecking no # 不做严格的host key check
    ControlMaster auto # 连接复用
    ControlPath ~/.ssh/sockets/%r@%h:%p
    ControlPersist 600
    ProxyJump <Host> # 指定中转设备
```

## cli
### scp
#### 历史遗留问题
##### scp上传速率慢, 下载速率正常
### ssh
#### 参数
- `-t <commands>`: 连上远端之后执行指定命令