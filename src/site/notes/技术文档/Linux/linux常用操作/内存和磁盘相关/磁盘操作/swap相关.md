---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/swap相关/","dg-note-properties":{}}
---

# 常用命令
# `swapon`
# `swapoff`

# 常见实例
## `Swap`扩容
**步骤**
1. 关闭swap
	- `swapoff <SWAP FILE>`
2. 扩大文件系统
	- `sudo dd if=/dev/zero of=<SWAP FILE> bs=1M count=8192 status=progress`
3. 重新初始化swap头
	- `sudo chmod 600 <SWAP FILE>`
	- `sudo mkswap <SWAP FILE>`
4. 启用swap
	- `sudo swapon <SWAP FILE>`
5. 验证
	- `free -h`
	- `sudo swapon --show`
