---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/串口相关/ser2net命令/","dg-note-properties":{}}
---

# 背景
- 一个串口转网络代理工具
- 它的核心功能是充当一座桥梁，让远程的计算机可以通过网络（通常是TCP/IP）来访问和使用本地物理串口（如 `/dev/ttyS0`, `/dev/ttyUSB0`
- 可以把它理解为一个“串口服务器”。
# 配置
## ser2net.yaml
- 版本限制在`>=4.0`
### 基本格式
```yaml
connection: &con01
  accepter: tcp,20108
  connector: serialdev,/dev/ttyACM0,115200n81,local
```
### 字段
-  `connection`: 定义锚点, 可以复用
	-  `accepter`: 定义协议和端口
		- 协议
			- `tcp`
	- `connector`: 定义连接到的串口设备及参数，格式为 serialdev,设备路径,波特率及格式,模式。例如 115200n81 表示 115200 波特率, 8 数据位, 无校验, 1 停止位；local 表示本地模式，不考虑 DTR/DCD 等信号
## ser2net.conf
- 版本限制在`<4.0`
### 基本格式
```shell
20108:raw:0:/dev/ttyACM0:115200 8DATABITS NONE 1STOPBIT
```
### 字段
- 监听的tcp端口
- 协议
	- `raw`: 原始数据
	- `telnet`: 解析`telnet`协议数据
	- 超时时间
		- 0表示永不超时
	- 串口设备路径
	- 波特率
	- 数据bit位
	- 校验bit位
	- 停止bit位
# 参数
- `-C <config line>`: 直接指定配置, 一行搞定
- `-c <config file>`: 从配置文件加载配置 
- `-n`: 前端运行服务
# 实例
- `eg. ser2net -C "2001:telnet:0:/dev/ttyS1:115200 NONE 1STOPBIT 8DATABITS XONXOFF LOCAL -RTSCTS max-connections=10" -n`