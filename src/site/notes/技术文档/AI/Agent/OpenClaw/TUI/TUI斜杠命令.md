---
{"dg-publish":true,"permalink":"/技术文档/AI/Agent/OpenClaw/TUI/TUI斜杠命令/","dg-note-properties":{}}
---

# new
- 重新打开一个会话, 之前的会话内容会全部清空
	- 可用于减少token输入
# status
- 查看当前会话状态, 包括
	- 正在使用的模型
	- 已消耗的`Token`数量, 会话`Token`参考[[技术文档/AI/Agent/OpenClaw/常见问题/Token含义和关系\|Token含义和关系]]
	- `...`
# 输出解析
- openclaw tui 表示当前在TUI界面中，后面是WebSocket连接地址，agent名，session名。
- session agent:main:main 表示当前会话的标识。
- Gateway status 网关状态，显示链路通道未知（Link channel: unknown），可能是没有连接任何外部频道（如Telegram等），因为刚部署。
- Heartbeat: 30m (main) 心跳间隔30分钟，针对main agent。
- Session store: 会话存储文件路径。
- Default model: 默认模型及上下文长度。
- Active sessions: 当前活跃会话数1。
- Recent sessions: 最近的会话详情：会话标识、类型是direct（直接对话），多久前，模型，已用token/上限，剩余，百分比，flags，id。
- Queued system events: 排队系统事件，显示有一个网关重启更新被跳过，原因不是git安装，建议运行openclaw doctor。
- 最后状态行：连接状态、空闲、agent、session、模型、token使用情况。
# compact
- 用于压缩对话历史为一个摘要, 保留关键信息
	- 可以在不想丢失上下文的同时, 减少Token占用
## 基本格式
- `/compact [indication info]`
	- `indication info`: 指示信息, 告诉它哪些信息必须保留
		- 比如, 请保留我们刚才讨论的代码片段和最终的解决方案