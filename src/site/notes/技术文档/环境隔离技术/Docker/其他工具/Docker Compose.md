---
{"dg-publish":true,"permalink":"/技术文档/环境隔离技术/Docker/其他工具/Docker Compose/","dg-note-properties":{}}
---

# 背景
- 可以把容器的构建配置以文件的形式编排
- 参考(https://www.cnblogs.com/mrhelloworld/p/docker13.html)
# 配置
## docker-compose.yml
```yaml
services:
	<SERVER NAME>: # eg. gitlab
		build: <PATH> # 如果镜像还没构建, 指定 Dockerfile 所在的路径[reference:8]
		image: <IMAGE> # eg. gitlab/gitlab-ce:16.5.3-ce.0
		container_name: <CONTAINER NAME> # eg. gitlab
		restart: <START MODE> 
		# START MODE		
			# always: 开机自启
			
		ports: # 端口映射
			- '<LOCAL_PORT:HOST_PORT>'
		volumes: # 卷映射
			- '<LOCAL_DIR/FILE:HOST_DIR/FILE>'
		
		# 容器系统资源类
		shm_size: # 最大共享内存, eg. 256m
		mem_limit: # 最大内存占用, eg. 2g
		memswap_limit: # 最大内存swap占用, eg. 2g
		cpus: # 最大cpu核心数, eg. 2
		pids_limit # 最大创建的pid数量, eg. 600 
		
		# 权限类
		# 相当于给了容器里的进程“宿主机 root 用户”的几乎全部权限，直接打破了 Docker 默认的诸多安全隔离限制
		# 1. 直接访问宿主机所有硬件设备
		# 2. 可以挂载文件系统分区
		privileged: # ture or false
		user: # 指定运行容器进程的UID或者用户名 eg. rk
		group_add: # 给当前用户添加组, 不建议在这里修改权限, ssh连接会丢失属组
			- # 字符串或数字, 即组名或者组ID, eg. 1000 or sudo
		
		# shell类
		environment: # 设置环境变量
			<ENV_VAR>:<VALUE>
		
		tty: # 是否分配伪终端, 对应-t, true or false
		stdin_open: # 是否接受标准输入, 对应-i, true or false
		command: <COMMAND> # 容器启动的主命令
		working_dir: # 工作目录
```
### 常见问题

**容器启动直接退出**


**SHELL变量转义**
使用`$$`

# 使用
## 命令
**基本格式**
`docker compose <OPTIONS>`

**位置参数**
- `run <container name> <shell bin>`: 创建并交互式启动容器, `eg. docker compose run atk_dlrk3506b_sdk /bin/bash`
	- `--rm`: 交互式`shell`退出, 自动删除容器 
- `up`: 创建并启动容器和网络, 保留卷
	- `-d`: 后台启动, 不占用前台资源
- `down`: 停止并删除容器和网络, 保留卷

**可选参数**