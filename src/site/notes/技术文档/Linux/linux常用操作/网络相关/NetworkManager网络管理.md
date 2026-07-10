---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/NetworkManager网络管理/","dg-note-properties":{}}
---

# 下载安装
# 配置
不推荐直接修改配置, 请用`nmcli`命令
# 服务程序

# 客户端程序
## nmcli

### 子命令
#### device
##### status
查看可用网卡设备
#### connection
##### add
增加一个网络连接的配置
- **实例**
	- `eg. sudo nmcli connection add type ethernet con-name "my-dhcp-enp0s3" ifname enp0s3 ipv4.method auto`
##### up
使配置生效
##### show
 列出内存和磁盘中存储的关于网络连接的配置信息
##### modify
 重新配置一个网络连接的配置, 并持久化存储
- **基本格式**
	- `nmcli connection modify <NAME> <OPTIONS>`
- **位置参数**
	- `ipv4.route-metric <NUMBER>`
- **可选参数**
- **实例**
	- 改`connection`名称
		- `eg. sudo nmcli connection modify "原连接名" con-name "新连接名"`

---
1. 背景

2. ssid是什么？

3. 配置

4. 路径

5. /etc/NetworkManager/

6. 文件 //NetworkManager.conf

7. 注意

8. 文件内容

9. 实例

10. managed=false

11. 作用

12. 表示不管理/etc/network/interfaces中定义的网络接口

13. /etc/NetworkManager/system-connect

14. 文件 // format: <file name>.nmconnection

15. 注意

16. 每个网络接口对应一个文件

17. eg. eth0.nmconnection

18.  文件内容

19. 注意

20. 不额外标注生效方法，就是上同

21. 实例

22. 配置网络接口真实名称以及在NetworkManager中的名称

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