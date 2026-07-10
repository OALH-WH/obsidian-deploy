---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/系统相关/systemctl命令/","dg-note-properties":{}}
---

# 背景
- 控制`systemd`管理的服务
# 电源管理
## 参数
- `poweroff`: 关机并切断电源
# 服务控制
## 参数
- `cat`: 查看服务配置, 如需修改可通过参数`edit`
- `edit`: 修改服务配置, `eg. systemctl edit tftpd-hpa.service`
- `restart`: 重启服务
- `daemon_reload`: 重新加载配置文件
- `stop`: 停止服务
- `start`: 启动服务
- `enable`: 设置开机自启
- `disable`: 设置开启禁止自启
- `status`: 查看服务状态
	- 内容解析
		- 列
			- Loaded
				- 服务配置路径
				- 开启是否自启
				- `preset`: ?
			- Active
				- 服务当前状态
			- ...
---
1. 配置文件
2. /etc/systemd/system

3. 该目录下记录了各个服务的配置文件

4. /lib/systemd/system

5. 该目录下为实际执行服务命令的位置

6. API

7. systemctl daemon-reload:重新加载配置文件

8. 实例

9. 重新加载配置文件的内容

10. eg. systemctl daemon-reexec ssh.service

11. 添加服务到systemd

12. systemctl enable <serve>

13. 列出所有服务

14. systemctl list-units --type=service --all

15. 设置服务开机自启

16. eg. systemctl enable ssh.service

17. 检查服务是否开机自启

18. eg. systemctl is-enabled ssh.service

19. 设置服务的配置文件

20. eg. systemctl edit ssh.service