---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/IP相关/ip命令/","dg-note-properties":{}}
---


# 占位符
## DEV
表示网络接口, `eg. eth0, eth1...`

# 子命令
---
## neigh
等价[[技术文档/Linux/linux常用操作/网络相关/IP相关/arp命令\|arp命令]]
查看`arp`缓存表
### 基本格式
**位置参数**
- `show`: 查看`arp`表
- `flush`:
	- `dev <DEV>`: 删除指定网络接口的`arp`缓存
	- `to <PREFIX>`: 可精确匹配`ip addr`删除

### 字段解析
`eg. 192.168.0.59 dev eth2 lladdr c8:58:b3:79:e4:0b REACHABLE`
- `field 1`: `ip`地址
- `field 2`
- `...`
- `field 5`: 物理地址, 参考[[技术文档/计算机网络相关/OSI七层模型/链路层/协议/ARP协议#MAC地址\|ARP协议#MAC地址]]
- `field 6`: 当前条目的状态
	- `REACHABLE`: 最近确认
	- `STALE`: 之前可达, 直至目前网络通信处于空闲状态
	- `FAILED`: 

### 实例
```shell
# 清空所有arp缓存
ip neigh flush all
# 清空eth0 arp缓存
ip neigh flush dev eth0
# 清除192.168.0.1 arp缓存
ip neigh flush to 192.168.0.1
```
---
# 参数
# 常见实例

## 查看ARP表, ARP作用
### 参考
- [[链路层#ARP协议\|链路层#ARP协议]]
### 命令
```shell
ip neigh show
```
## 对某个网络接口添加IP地址
### 命令
```shell
sudo ip addr add 192.168.1.100/24 dev eth0
```
## 删除某个网络接口的指定IP地址
### 命令
```shell
sudo ip addr del 192.168.1.100/24 dev eth0
```
## 路由相关
### 添加默认路由
#### 命令
```shell
sudo ip route add default via 192.168.1.1 dev eth0
```
# 数据分析