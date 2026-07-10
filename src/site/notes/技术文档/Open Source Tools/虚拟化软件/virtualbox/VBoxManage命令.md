---
{"dg-publish":true,"permalink":"/技术文档/Open Source Tools/虚拟化软件/virtualbox/VBoxManage命令/","dg-note-properties":{}}
---

# 背景
# 位置参数
- `startvm <VIRTUAL MACHINE NAME>`
- `list vms`: 列出注册的虚拟机
# 可选参数
- `--type headless`
# 示例
## 查看注册的虚拟机
- `eg. VBoxManage list vms`
## 启动注册好的虚拟机
- 以无界面启动
	- `eg. VBoxManage startvm test_machine --type headless`
