---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/设备管理/udev设备管理/","dg-note-properties":{}}
---

# 背景
# 依赖
# 安装
# 配置
## rules.d
位于`/etc/udev/rules.d`, 文件通常以`.rules`结尾
文件名中的数字决定了规则处理的优先级, 数字越小越先执行

**常用操作符**

|操作符|类型|描述|示例|
|---|---|---|---|
|`==`|比较|用于**匹配**，检查键的值是否**等于**指定的值[](https://docs.oracle.com/en-us/iaas/oracle-linux/udev/ol-udev-working-with-udev-rules.htm#1)。|`ACTION=="add"`|
|`!=`|比较|用于**匹配**，检查键的值是否**不等于**指定的值[](https://docs.oracle.com/en-us/iaas/oracle-linux/udev/ol-udev-working-with-udev-rules.htm#1)。|`KERNEL!="sda"`|
|`=`|赋值|**覆盖**赋值，将键的值设为指定值[](https://docs.oracle.com/en-us/iaas/oracle-linux/udev/ol-udev-working-with-udev-rules.htm#1)[](https://manpages.debian.org/testing/udev/udev.7.en.html#1)。|`MODE="0660"`|
|`+=`|赋值|**追加**赋值，将值添加到键的值列表中[](https://docs.oracle.com/en-us/iaas/oracle-linux/udev/ol-udev-working-with-udev-rules.htm#1)[](https://manpages.debian.org/testing/udev/udev.7.en.html#1)。|`SYMLINK+="my_disk"`|
|`:=`|赋值|**最终**赋值，设置后，后续规则无法再修改此键的值[](https://docs.oracle.com/en-us/iaas/oracle-linux/udev/ol-udev-working-with-udev-rules.htm#1)[](https://manpages.debian.org/testing/udev/udev.7.en.html#1)。|`OPTIONS:="nowatch"`|
**常用替换变量与模式匹配**
- **替换变量**：在规则值中可使用的动态变量。
    - `$devnode` 或 `%N`：当前设备的节点名，如 `/dev/sdb1`。
    - `$kernel` 或 `%k`：设备的内核名称，如 `sdb1`。
- **模式匹配**：在匹配值中可使用通配符[](https://docs.oracle.com/en-us/iaas/oracle-linux/udev/ol-udev-working-with-udev-rules.htm#1)。
    - `*`：匹配任意数量的任意字符。
    - `?`：匹配任意**一个**字符。
    - `[]`：匹配括号内的任意一个字符，如 `[0-9]`。

**常见变量替换**

| 变量            | 简写形式       | 描述                     | 示例值                               |
| ------------- | ---------- | ---------------------- | --------------------------------- |
| `$kernel`     | `%k`       | 设备的内核名称                | `sdb1`                            |
| `$number`     | `%n`       | 设备的内核序号                | `1` (对于 `sdb1`)                   |
| `$devpath`    | `%p`       | 设备的 devpath            | `/devices/pci/.../block/sdb/sdb1` |
| `$attr{file}` | `%s{file}` | 设备的 sysfs 属性值          | `$attr{size}` 获取设备大小              |
| `$env{key}`   | `%E{key}`  | 设备的环境变量/属性值            | `$env{ID_FS_UUID}` 获取文件系统 UUID    |
| `$major`      | `%M`       | 设备的主设备号                | `8`                               |
| `$minor`      | `%m`       | 设备的次设备号                | `17`                              |
| `$result`     | `%c`       | 由 `PROGRAM` 程序返回的字符串   | `12345`                           |
| `$parent`     | `%P`       | 父设备的节点名                | `sdb`                             |
| `$root`       | `%r`       | udev_root 的值           | `/`                               |
| `$sys`        | `%S`       | sysfs 的挂载点             | `/sys`                            |
| `$$` / `%%`   | -          | 转义字符，分别表示 `$` 和 `%` 本身 | -                                 |

**示例**
```shell
ACTION=="add", \
SUBSYSTEMS=="usb", \
SUBSYSTEM=="block", \
ENV{ID_FS_USAGE}=="filesystem", \
RUN{program}+="/usr/bin/systemd-mount --no-block --automount=yes --collect $devnode /media"
```
**匹配条件** 
- `ACTION`: 设备行为, 常见的有
	- `add`: 插入
	- `remove`: 拔出
	- `change`: 属性变化
- `KERNEL`: 匹配内核给设备起的名称, `eg. sda1, ttyUSB0`
- `SUBSYSTEMS`: 匹配设备所属子系统, `eg. block, usb, tty`
	- `usb`: 一般为`usb`设备
	- `block`:
	- `net`: 
- `ATTR{key}`: 匹配`/sys`下该设备自身的属性, `eg. ATTR{size}=="1024"`表示匹配大小为1024个扇区的设备
	- `idVendor`: 厂商ID
		- `usb`设备参考[[技术文档/Linux/linux常用操作/USB相关/lsusb命令#^9d79da\|lsusb命令#^9d79da]]
	- `idProduct`
		- `usb`设备上同
- `ENV{key}`: 匹配环境变量
**匹配行为**
- `MODE`: 设置设备文件的**权限模式**（八进制）。`MODE="0666"` 表示任何人都可以读写（rw-rw-rw-)
- `OWNER`: 设置设备的属主
- `GROUP`: 设置设备的属组
	- `plugdev`: 设置设备文件的属组为`plugdev`
- `SYMLINK`: 在 `/dev/` 下创建一个**软链接**（别名)
	- `+=`: 保留当前链接列表, 新增一个符号链接
- `RUN{type}`: 指定要执行的程序类型, 常见的有
	- `program`: 默认类型, 执行外部程序或脚本, 可以简写为`RUN=`
	- `builtin`: 执行`udev`内置的程序, 而不是外部程序
# 使用

## 常见命令
### udevadm
#### 基本格式

**位置参数**
- `control`
	- `--reload-rules`: 重载`rules`规则
- `trigger`: 通常和`udevadm control --reload-rules`一起使用
- `info`: 获取设备在`udev`的信息
	- `--attribute-walk`: 只显示属性, 即`ATTR`
	- `--name`: 通过设备节点匹配设备信息
	- `--path`: 通过`sysfs`路径查找设备信息

**示例**
```shell
# 1. 查看设备的基本USB信息（获取idVendor和idProduct）
lsusb
# 输出：Bus 001 Device 002: ID 2207:3115 (类似这个，2207是Rockchip厂商ID)

# 2. 查看该USB设备在udev眼中的详细属性（找出所有可用匹配键）
udevadm info --attribute-walk --name=/dev/bus/usb/001/002
```