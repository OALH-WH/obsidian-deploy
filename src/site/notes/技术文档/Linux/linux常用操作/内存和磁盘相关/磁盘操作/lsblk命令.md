---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/lsblk命令/","dg-note-properties":{}}
---

# 背景
- **块设备上的文件系统**
# 作用
- 以树状图的形式列出,系统中素有的块设备及其依赖关系
- 只读, 非常安全
- 没有文件系统和分区也能显示
# 参数
- `-f`: 显示文件系统信息(类型, 标签即label, UUID), 如果没有显示就执行`eg. blkid dev/sda1`
- `-p`: 显示设备的完整路径(eg. /dev/sda1)
# 使用
# 内容解析
## 列
- `NAME`: 设备文件名/设备文件路径
- `FSTYPE`: 文件系统类型
	- `swap`: 表示用于临时存放内存中不活跃的数据的文件系统
	- ext2
	- ext4
	- `LVM2_member`: 表示这是一个使用LVM管理的逻辑卷组, 参考[[技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/LVM(Logical Volume Manager，逻辑卷管理器)\|LVM(Logical Volume Manager，逻辑卷管理器)]]
	- iso9660
- `FSVER`文件系统版本
- `FSAVAIL`: 可用大小
- `FSUSE`: 存储使用率
- `MOUNTPOINTS`: 挂载点
- `LABEL`
- `UUID`
## 示例1
```shell
(venv) sino@debian12:~/work/venv/projects/uaonos$ lsblk -f
NAME                    FSTYPE      FSVER            LABEL        UUID                                   FSAVAIL FSUSE% MOUNTPOINTS
sda                     swap        1                             aa1a6e1c-d7e2-4c47-b23f-3acb25fb6331                  [SWAP]
sdb                                                                                                                     
├─sdb1                  ext2        1.0                           b1976272-1538-4de3-a175-2eba77001dc5    371.9M    13% /boot
├─sdb2                                                                                                                  
└─sdb5                  LVM2_member LVM2 001                      QNKdKE-XKF4-4elv-vR6y-lqHC-hv5R-l4jk2w                
  ├─debian12--vg-root   ext4        1.0                           c0753f26-7723-4222-a179-60d9ddb4711b    374.4G     6% /
  ├─debian12--vg-swap_1 swap        1                             a5cdc6aa-282b-4fb5-a60a-91c56edf12fd                  
  └─debian12--vg-home   ext4        1.0                           e7806e80-df4f-40a7-8043-7fc799be0d18    336.5G    26% /home
sr0                     iso9660     Joliet Extension GParted-live 2018-12-14-00-48-58-00 
```