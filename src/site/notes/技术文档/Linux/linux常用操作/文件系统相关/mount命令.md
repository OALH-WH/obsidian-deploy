---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文件系统相关/mount命令/","dg-note-properties":{}}
---

# 背景
- **uuid(universal unique identifie)**: 通用唯一性标识符
- **label**: 用户自定义标识
- **uuid**和**label**可以通过命令`lsbkl -f`查看 (参考[[技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/lsblk命令\|lsblk命令]])
# 作用
# 基本格式
`mount [options] <src> <tar>`

**options**
- `--bind`
- `-t, --types <list>`: 指定处理的文件系统, 获取支持挂载的文件系统参考[[技术文档/Linux/常见目录和文件作用#filesystems：显示内核支持的文件系统模块\|常见目录和文件作用#filesystems：显示内核支持的文件系统模块]]
- `[--source] <src>`: 指定挂载源(path, label, uuid, 其中path是随机的, 当增加或者移除一块硬盘, 之前的path可能不存在, 因此label和uuid可能更加可靠 )
- `[--target] <target>`: 指定挂载点, 即挂载的位置
- `-a, --all`: 挂载所有在`fstab`中定义好的文件系统(会读取配置文件`/etc/fstab`)
- `[-o opt1,opt2]`: 指定挂载选项
	- `ro/rw`: 挂载权限, 只读挂载或者读写挂载
	- `remount`: 重新挂载
	- `nolock`: 
	- `errors=<option>`: 挂载失败的处理
		- `remount-ro`: 重新只读挂载
		- 
# 示例
```shell
# 把设备mtd1使用ext4文件系统挂载到根目录/下
mount -t ext4 /dev/mtd1 /
or
mount -t ext4 --source /dev/mtd1 --target /
or
mount -t ext4 /dev/mtd1 / -o ro # 只读挂载, 文件不可写
or
mount -t nfs4 /dev/mtd1 /
or
mount -t nfs 192.168.1.200:/... /
or
mount # 查看所有已经挂载的文件系统, 包括挂载选项, 文件系统类型, 挂载点以及块设备(path or UUID or LABEL)
or
mount -o remount,rw / # 重新读写挂载根文件系统
```