---
{"dg-publish":true,"permalink":"/技术文档/Linux系统常见构建工具/Buildroot/常见问题/vscode无法连上设备/","dg-note-properties":{}}
---

# 问题1: 非交互模式下PS1变量也不为空
- 解决方案
	- 修改PS1设置逻辑, 非交互模式下设置为空, 禁止export
# 问题2: tar软件包不为GNU格式
- 解决方案
	- 修改buildroot的tar包配置为使用GNU格式