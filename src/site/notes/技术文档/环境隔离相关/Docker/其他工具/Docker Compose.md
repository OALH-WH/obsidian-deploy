---
{"dg-publish":true,"permalink":"/技术文档/环境隔离相关/Docker/其他工具/Docker Compose/","dg-note-properties":{}}
---

# 背景
- 可以把容器的构建配置以文件的形式编排
- 参考(https://www.cnblogs.com/mrhelloworld/p/docker13.html)
# 配置
## docker-compose.yml
```yaml
services:
	<SERVER NAME>: # eg. gitlab
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
		
		# shell类
		environment: # 设置环境变量
			<ENV_VAR>:<VALUE>
		
		tty: # 是否分配伪终端, true or false
		command: <COMMAND> # 容器启动的主命令
```
### 常见问题

**SHELL变量转义**
使用`$$`
### 基本格式
### 字段解析
- `entrypoint`: 

# 使用
## 命令
**基本格式**
`docker compose <OPTIONS>`

**位置参数**
- `up`: 创建并启动容器和网络, 保留卷
- `down`: 停止并删除容器和网络, 保留卷

**可选参数**