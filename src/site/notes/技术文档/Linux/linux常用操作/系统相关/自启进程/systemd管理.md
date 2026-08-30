---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/系统相关/自启进程/systemd管理/","dg-note-properties":{}}
---

# 背景
## target
在 systemd 体系中，**Target（启动目标）** 替代了传统 SysVinit 的「运行级别（Runlevel）」，每个 Target 定义了一组需要启动的服务和系统状态，对应不同的使用场景

通过`systemctl set-default/get-default`查看和修改当前默认的运行级别, 具体参考[[技术文档/Linux/linux常用操作/系统相关/systemctl命令\|systemctl命令]]

| Target 名称           | 对应传统运行级别 | 说明                 |
| ------------------- | -------- | ------------------ |
| `graphical.target`  | 运行级别 5   | 图形桌面模式，带桌面环境，个人版默认 |
| `multi-user.target` | 运行级别 3   | 多用户纯命令行模式，服务器版默认   |
| `rescue.target`     | 运行级别 1   | 单用户救援模式，用于系统修复     |
| `poweroff.target`   | 运行级别 0   | 关机                 |
| `reboot.target`     | 运行级别 6   | 重启                 |

# 配置
## .service

**示例**
```shell

```

## .automount
起名要跟`Where`保持一致, `eg. Where=/mnt/u30pro -> mnt-u30pro.automount`
配置文件位于`/etc/systemd/system`目录
触发器：访问目录时自动执行 mount

启动这个配置通过`systemctl enable mnt-u30pro.automount`, 启动`automount`就不用启动`mount`

**示例**
```shell
[Unit]
Description=automount描述

[Automount]
# 监控哪个目录，必须和.mount的Where完全一致
Where=/mnt/u30pro
# 闲置多久自动卸载，秒；0=不自动卸载
TimeoutIdleSec=60

[Install]
# 开机随多用户模式启用
WantedBy=multi-user.target

```
## .mount
起名要跟`Where`保持一致, `eg. Where=/mnt/u30pro -> mnt-u30pro.mount`
配置文件位于`/etc/systemd/system`目录
定义挂载本身，等价于 mount 命令参数

**示例**
```shell
[Unit]
# 描述
Description=描述文本
# 依赖：在某目标之后启动
After=xxx.service
# 拉取依赖，要求xxx启动
Wants=xxx.service
# 强依赖，xxx失败本单元也失败
Requires=xxx.service

[Mount]
# 源设备/网络地址，对应mount源
What=//192.168.0.1/U30 Pro
# 挂载点，必须真实存在目录
Where=/mnt/u30pro
# 文件系统类型：cifs / nfs / ext4 / vfat / fuse
Type=cifs
# mount -o 的参数，逗号分隔
Options=credentials=/etc/cifs_u30.cred,vers=2.1,_netdev,uid=1000,gid=1000
# or Options=username=root,password=1234567890,vers=2.1,_netdev,uid=1000,gid=1000

# 是否读写：rw ro；一般放在Options里
# ReadWrite=rw

# 不要写 [Install] ！！
# 如果被automount管理，.mount单元绝对不能写[Install]段

```


# 启动