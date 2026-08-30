---
{"dg-publish":true,"permalink":"/技术文档/虚拟化软件/virtualbox/VBoxManage命令/","dg-note-properties":{}}
---

# 背景
# 基本格式
**位置参数**
- `startvm <VIRTUAL MACHINE NAME>`
- `list vms`: 列出注册的虚拟机
- `list runningvms`: 列出正在运行的虚拟机
- `showvminfo <VM name>`: 列出指定虚拟机的属性
	- `VM name`可通过`list vms`查看
- `controlvm <VM name>`: 控制虚拟机
	- `reset`: 控制虚拟机重启
**可选参数**
- `--type headless`
**示例**
查看串口属性
- `eg. VBoxManage showvminfo ... | findstr UART`

查看是否运行
- `eg. VBoxManage showvminfo ... | findstr State`

查看注册的虚拟机
- `eg. VBoxManage list vms`
- 
启动注册好的虚拟机
- 以无界面启动
	- `eg. VBoxManage startvm test_machine --type headless`
