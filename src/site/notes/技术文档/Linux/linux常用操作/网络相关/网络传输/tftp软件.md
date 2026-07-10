---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/网络传输/tftp软件/","dg-note-properties":{}}
---

# 安装
- 可通过[[技术文档/Linux/linux常用操作/软件包管理/apt包管理/使用#`apt-file`命令|apt-file]]命令检索包名
- `tftpd-hpa`: kali发行版软件包名

**服务**
- `tftp-hpa.service`: 服务名

**程序**
- `in.tftpd`: 实际执行的程序名
# 配置
## `/etc/default/tftp-hpa`
- `TFTP_DIRECTORY=<DIR PATH>`:指定TFTP服务的文件根目录 
- `TFTP_OPTIONS`: 服务器功能选项, `eg. TFTP_OPTIONS="--secure --create"`
	- `--secure`: ???
	- `--create`: 允许上传文件
	- `--blocksize 8192`: ???
	- `--timeout 300`: 设置超时时间

# 客户端
## 命令
### `tftp`
### 基本格式
- `tftp [-4][-6][-v][-l][-m mode] [host [port]] [-c command]`
#### 常见参数
- `-c <command>`
	- `help [<command>]`: 获取帮助信息
	- `get <SERVER PATH>`: 从tftp服务上获取文件
	- `put <LOCAL PATH> <SERVER PATH>`: 上传文件到tftp服务里
# 常见问题
## 服务启动失败, 检测不到指定的`tftp`目录
如果是`systemctl`管理, 通过`systemctl cat tftpd-hpa`检查管理配置, 如果`ProtectHome=yes`，会阻止服务访问`/home/`下的任何目录, 修改参考