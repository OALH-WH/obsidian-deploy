---
{"dg-publish":true,"permalink":"/技术文档/硬件通信协议/SPI/","dg-note-properties":{}}
---

# 背景
- SPI, Serial Peripheral Interface, 串行外设接口
## 协议特点
- 高速, 全双工, 同步的通信总线
- 一主多从
## 物理接线
- 可以是3/4线式
### 4线式
#### 主机
- 时钟线, SPICLK/SCLK
- 片选线, CS(主机输出)
- 从机输入, 主机输出线, MOSI
- 主机输入, 从机输出线, MISO
#### 从机
- 时钟线, SPICLK/SCLK
- 片选线, CS(主机输出)
- 从机输入, 主机输出线, SDI
- 主机输入, 从机输出线, SDO
#### 菊花链模式
- 所有从机的片选信号线连接在一根`CS`总线上
- 第一个从机的SDO线连接第二个从机的SDI线, 依此类推
- 当主机给`CS`总线发送信号时, 由第一个从机接收再转发给第二个从机, 依次类推
![Pasted image 20260316203115.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E7%A1%AC%E4%BB%B6%E9%80%9A%E4%BF%A1%E5%8D%8F%E8%AE%AE/resources/Pasted%20image%2020260316203115.png)
#### 常规模式
- 所有从机的片选信号线对应主机上一根单独的`CS`总线
![Pasted image 20260316203123.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E7%A1%AC%E4%BB%B6%E9%80%9A%E4%BF%A1%E5%8D%8F%E8%AE%AE/resources/Pasted%20image%2020260316203123.png)
# 配置
## 时钟极性, CPOL, Clock Polarity
- 决定空闲时的**时钟线电平高低**
### CPOL = 0
- 时钟线空闲时, 为**低电平**
### CPOL = 1
- 时钟线空闲时, 为**高电平**
## 时钟相位, CPHA, Clock Phase
- 决定**数据采样/移出的模式**
- 采样: 指接收方在时钟的某个边沿（上升沿或下降沿）**读取**数据线上的电平值，并将其锁存到移位寄存器中。简单来说，就是“看”数据线此时是 0 还是 1。
- 移出: 指发送方在时钟的某个边沿**改变**数据线上的电平，将下一位数据放到总线上。旧的数据位被“移除”，新的数据位被“放置”出来。
### CPHA = 0
- 表示处于低电平时为空闲状态, 所以**上升沿采样, 下降沿移出**
### CPHA = 1
- 表示处于高电平时为空闲状态, 所以**下降沿采样, 上升沿移出**

# 时序
## 起始条件
- `SCLK`线为空闲状态时, 拉低从机的`CS`线
## 停止条件
- `SCLK`线为空闲状态时, 拉高从机的`CS`线
# 读/写模式
# 示例
## CPOL = 0, CPHA = 0
![Pasted image 20260316211913.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E7%A1%AC%E4%BB%B6%E9%80%9A%E4%BF%A1%E5%8D%8F%E8%AE%AE/resources/Pasted%20image%2020260316211913.png)
# 扩展
## QUAD SPI, QSPI
## DUAL SPI, DSPI
---
20. DSPI（Dual SPI）:只针对SPI Flash，并不是针对所有的SPI外设

21. QSPI（Queued SPI）（半双工）

22. 线路模式

23. 3线Single Wirte/Read模式

24. 4线Single Write/Read，Dual Read模式

25. 6线Single Quad Read模式

26. 工作模式

27. 间接模式：使用QSPI寄存器执行全部操作

28. 状态轮询模式：周期性读取外部Flash状态寄存器，而且标志位置1时会产生中断

29. 内存映射模式：外部Flash映射到微控制器地址空间，从而系统将其视作内部存储器，采用双闪存模式时，将同时访问两个Quad-SPI Flash，吞吐量和容量均可提高

30. QPI（全双工，QSPI的扩展或者说是变种）