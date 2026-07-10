---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/内存和磁盘相关/磁盘操作/LVM(Logical Volume Manager，逻辑卷管理器)/","dg-note-properties":{}}
---

# 背景
- Linux 系统的一种**高级磁盘存储管理方案**
# 依赖
## Linux内核配置
## 当根文件系统也使用LVM管理(可选)
### **initramfs** 支持

# 安装
## 方式1:  Apt包管理器
```shell
sudo apt install lvm2

# 验证安装
sudo pvdisplay --version
```
## 方式2: Buildroot 配置
# 使用
## 个人理解
- 扩展已经格式化好的逻辑卷
## 核心要点
### **物理卷（Physical Volume, PV）**
- 硬盘或分区的"原材料", 是LVM管理的底层存储单元
#### 示例
```shell
# 把物理硬盘或分区初始化为物理卷
sudo pvcreate /dev/sdb1
sudo pvdisplay  # 查看物理卷
```
### **卷组（Volume Group, VG）** 
- 创建一个统一的存储池, 所有物理卷的空间在这里合并
#### 示例
```shell
# 将多个物理卷组合成一个“存储池”
sudo vgcreate myvg /dev/sdb1 /dev/sdc1
sudo vgdisplay  # 查看卷组
```

### **逻辑卷（Logical Volume, LV）**
- 从存储池划分出来可动态调整的逻辑分区
#### 示例
```shell
# 从卷组中划分出逻辑卷（类似分区）
sudo lvcreate -L 50G -n mydata myvg
sudo lvdisplay  # 查看逻辑卷
```
## 实例
### 将现有系统的根分区迁移到 LVM
**步骤**
1. 创建好新的`LVM`逻辑分区, 并挂载到一个空的目录
2. 复制根目录下所有文件到这个新的目录(需要在`live-os`下做)
	- 执行命令`rsync -aAxv /mnt/sda1/ /mnt/sda2/`, 把文件备份到新的`LVM`逻辑分区
3. 参考引导流程[[技术文档/Linux/Linux启动引导/引导流程#发行版\|引导流程#发行版]], 下述步骤按照`GRUB`引导描述
4. 挂载虚拟文件系统并`chroot`(保证运行状态和当前环境一致)
5. 修改`/etc/fstab`
6. 修改`GRUB`引导参数的`root`指向新的分区(保证内核启动时使用新的分区路径)
	1. 编辑`/etc/default/grub`, 找到`GRUB_CMDLINE_LINE_DEFAULT`, 替换`root=`部分
	2. 执行`update-grub`命令重新生成`GRUB`菜单
	3. 检查`/boot/grub/grub.cfg`中`root`参数是否正确
	4. 安装`GRUB`新的配置到引导磁盘
7. 配置`initramfs`, 使其提前加载`dm-mod`和`lvm`钩子, 在挂载根分区之前就激活`LVM`逻辑卷(保证能找到引导参数中`root`指定的分区路径)

**示例**
```shell
# step.4
mount --bind /dev  /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys  /mnt/sys

# 如果是 UEFI 系统，确保 efivars 可用（可能已挂载）
[ -d /sys/firmware/efi ] && mount --bind /sys/firmware/efi/efivars /mnt/sys/firmware/efi/efivars 2>/dev/null

chroot /mnt

# step.5


# BIOS 启动
# 修改grub配置, 修改完了之后执行
grub-update
# 安装到新的磁盘, 这里指定的是磁盘, 不是分区
grub-install /dev/sda

# UEFI 启动方式（需确认 EFI 分区已挂载，例如 /boot/efi）
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=Kali

# /dev/sda 应替换为实际系统引导磁盘（可通过 lsblk 查看哪个磁盘包含 /boot 或 EFI 分区）。

# step.6
echo "dm-mod" >> /etc/initramfs-tools/modules
# 写入文件
update-initramfs -u -k all
# 检查
lsinitramfs /boot/initrd.img-$(uname -r) | grep dm-mod


```

## 扩容已有的逻辑卷
```shell
# 创建物理卷
# 添加到已有逻辑卷所在的卷组
# 添加到逻辑卷
# 扩容逻辑卷的文件系统
## 如果是ext4文件系统
resize2fs /dev/<VGName>/<LVName>

```
## 常见命令
### `pvcreate`
- 把物理硬盘或分区初始化为物理卷
### `pvdisplay`
- 查看物理卷
---
## LVM 常用命令速查
```shell
# 查看系统 LVM 结构
sudo pvs    # 物理卷状态
sudo vgs    # 卷组状态
sudo lvs    # 逻辑卷状态
sudo lsblk  # 树形查看所有块设备

# 创建 LVM
sudo pvcreate /dev/sdX          # 创建物理卷
sudo vgcreate vg_name /dev/sdX  # 创建卷组
sudo lvcreate -L 50G -n lv_name vg_name  # 创建逻辑卷

# 调整大小
sudo lvextend -L +10G /dev/vg_name/lv_name  # 扩大逻辑卷
sudo lvreduce -L -10G /dev/vg_name/lv_name  # 缩小逻辑卷
sudo resize2fs /dev/vg_name/lv_name         # 调整文件系统（ext4）

# 添加新硬盘到现有 LVM
sudo pvcreate /dev/sdY
sudo vgextend vg_name /dev/sdY
# 现在新硬盘空间就可以分配给任何逻辑卷了
```


