---
{"dg-publish":true,"permalink":"/技术文档/AI/Agent/OpenClaw/openclaw命令/","dg-note-properties":{}}
---

# openclaw子命令
## doctor
### 可选参数
- `--fix`: 修复`openclaw`存在的错误
## update
## 
## dashboard
- 打开仪表盘
## tui
- 终端交互页面使用`openclaw`
## gateway
- `restart`: 重启网关
## browser
- 管理`openclaw`专用浏览器
### 位置参数
- `status`: 查看浏览器状态
- `start`: 启动专用浏览器
- `open <URL>`: 打开某个网页 
### 可选参数
- `--browser-profile <name>`: 指定浏览器预配置文件名, 可设置默认预设文件, `eg. browser.defaultProfile: "openclaw"`
	- `openclaw`: 托管的隔离浏览器
	- `chrome`: 到你系统浏览器的扩展中继
## skills
### 位置参数
- `list`: 显示已安装的`skill`
- `info <skill name>`: 查看`skill`详情
### 可选参数

