---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/IP相关/NetworkManager网络管理/","dg-note-properties":{}}
---

1. 背景

1. ssid是什么？

1. 配置

1. 路径

1. /etc/NetworkManager/

1. 文件 //NetworkManager.conf

1. 注意

1. 文件内容

1. 实例

1. managed=false

1. 作用

1. 表示不管理/etc/network/interfaces中定义的网络接口

1. /etc/NetworkManager/system-connect

1. 文件 // format: <file name>.nmconnection

1. 注意

1. 每个网络接口对应一个文件

1. eg. eth0.nmconnection

1.  文件内容

1. 注意

1. 不额外标注生效方法，就是上同

1. 实例

1. 配置网络接口真实名称以及在NetworkManager中的名称

```cpp
eg.1
[connection]
id=eth0 //设置id为eth0，如何使用?:eg.1 nmcli connection up <id>
interface-name=eth0 //绑定指定的网络接口
/**
 * @note 
 *   无线网卡在虚拟机中是默认桥接成有线接口，所以如果想用nmcli device wifi list查看ssid必然为空
 */
type=802-11-wireless //必须指定，否则不能正确加载配置文件，如果值是802-11-wireless，则必须要以下内容
[802-11-wireless]
ssid=...
```

1. 配置永久静态IP

1. 生效方式

1. 重启networkmanager服务/（nmcli重载配置+启动连接）

```json
eg.1
[ipv4]
method=auto //DHCP, 动态主机配置协议， 即自动分配IP地址

eg.2 静态分配ip地址
[connection]
id=eth0
interface-name=eth0
type=802-11-wireless

[ipv4]
address1=192.168.1.100/24,192.168.1.1
dns=8.8.8.8;114.114.114.114
ignore-auto-dns=true
method=manual
```

1. 使用

1. 命令

1. nmcli

1. 参数

1. device

1. wifi

1. list

1. 作用

1. 查看无线网络适配器的ssid

1. show

1. 作用

1. 查看网络接口信息

1. connection

1. load <config_file>

1. 作用

1. 从配置文件加载一个connection

1. delete <id|...>

1. 作用

1. 删除一个连接

1. show

1. 作用

1. 查看可用的网络接口

1. reload

1. 作用

1. 重新加载配置文件

1. up <配置文件名，eg. eth0.nmconnection>

1. 作用

1. 启用指定网络接口的连接