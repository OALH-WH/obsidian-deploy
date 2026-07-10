---
{"dg-publish":true,"permalink":"/技术文档/硬件通信协议/UART/","dg-note-properties":{}}
---

# 背景
- 小端传输bit位
- 全双工: 可同时收发
- 两根线: Tx和Rx
# 配置

# 数据传输格式
- 起始位: 1bit位, 逻辑`0`信号触发
- `LSB-MSB`数据位: 7bit位, 逻辑`0/1`信号
- 奇偶校验位: 1bit位, 逻辑
- 停止位: 1bit位 or 1.5bit位 or 2bit位, 逻辑`1`信号触发
- 空闲位: 1bit位, 处于逻辑`1`状态, 表示没有数据传输