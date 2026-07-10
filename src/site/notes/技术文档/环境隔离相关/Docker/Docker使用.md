---
{"dg-publish":true,"permalink":"/技术文档/环境隔离相关/Docker/Docker使用/","dg-note-properties":{}}
---

# 使用时常见问题
##  Docker容器中直接执行apt下载软件包找不到包
- 可能原因
	- Docker 镜像为了保持精简，**初始状态不包含最新的软件包列表**。不执行 `update` 就直接 `install`，就像去图书馆不查目录直接找书，很可能找不到

# 常见命令

## stats
查看容器的系统资源占用情况

### 基本格式
`docker stats <CONTAINER NAME | CONTAINER ID>`
## ps
查看容器的状态

**参数**
- `-a`: 关闭的容器也显示出来
- `--no-trunc`: 以不截断的方式显示
## inspect
查看容器的启动配置, 比如:
- `Volumes`: 表示创建镜像时, 目录挂载情况
- `Binds`: 表示容器运行时, 目录挂载情况
## volume
- 查看有哪些卷
## container

## update
- 设置容器的一些配置
### 基本格式
- `docker update`
### 参数
- `--restart=<action> <容器ID/NAME>`: 
	- `always`: 开启容器自启动
## logs
- 查看容器启动日志
### 基本格式
- `docker logs [options] <容器ID/NAME>`
### 参数
- `-f`: 实时显示, 类似`tail -f` 
## `builder`
### 参数
- `prune`: 清除构建缓存
---
## `system`
### 参数
- `prune`: 清除docker, 包括镜像, 容器, 缓存等
- `df`: 查看docker在磁盘中的使用情况, 包括镜像, 容器, 缓存等
### 示例
---
## `exec`
### 参数
### 示例
---
## `run`
- 从镜像启动为容器, 并指定启动参数
- 本质是一个进程
### 常见问题
- 当容器以类似`bash`作为启动命令时, 需要通过`-t`参数分配伪终端, 否则`bash` 认为自己是**非交互式**模式。它会执行完传入的命令（此处为无），然后立即退出（返回 0），导致容器状态变为 `Exited (0)`。
### 基本格式
- `docker run [OPTIONS]  <image name>:<label> <SHELL>`
### 参数
#### OPTIONS
- `-i`: 保持标准输入流打开, 允许向容器输入命令
- `-t`: 分配一个伪终端, 让shell感觉像在一个真实的终端里运行, 常和 `-i`一起使用
- `-p <local port>:<container port>`: 端口映射
- `--rm`: 容器退出时自动删除
- `--name <container name>`: 给容器起名字, 方便管理
- `--hostname`
- `-v <local_path:container_mount_path>[:OPTIONS]`: 指定挂载目录
	- `ro`: 只读挂载
	- `rw`: 读写挂载
- `--mount type=<TYPE>,source=<SRC>,target=<TAR>[,readonly]`: 指定挂载目录, 语法相较于`-v`语法更严谨, 比如`SRC`文件/目录不存在会报错, 而`-v`会直接创建
	- `TYPE`
		- `bind`
	- `SRC`: 宿主机路径, 可以精确到某个文件
	- `TAR`: 挂载的目标路径
- `-network`
#### SHELL
- `bash [OPTIONS]`
	- `-c <command>`: 在容器中执行某个命令
- `...`
- `sh`
### 示例

---
## start
启动暂停的容器
## rm
删除容器
删除容器
---
## `build`
- 注意最后需要指定构建上下文, `eg. .`表示当前目录
### 参数
- `--progress=plain`: 输出完整内容, 比如调试时执行的命令`RUN echo "..."`
- `--build-arg <stringArray>`: 设置构建时变量, 在`dockerfile`中引用通过`${}`
- `-t, --tag <stringArray>`: 设置构建出来的镜像名称和标签
	- `format`: name:tag
- `-f, --file <path string>`: 指定自定义构建配置文件名, `eg. ./Dockerfile.buildroot`
	- 默认使用Dockerfile作为构建配置文件名
	- **这里的路径基于指定的构建上下文, 比如上下文为当前目录., 则../Dockerfile.buildroot则时当前目录的父目录下所在的Dockerfile.buildroot**
	- 配置文件如何写参考[[技术文档/环境隔离相关/Docker/Docker配置\|Docker配置]]
### 示例
- `docker build -t buildroot-dev:latest -f Dockerfile.buildroot .`
#### 
---
## `pull`
- 拉取镜像
### 参数
### 示例
- 拉取 `hello-world`镜像
	- `docker pull hello-world`: 用来测试网络是否可用
---
## `info`
- 查看docker的一些配置信息
### 参数
### 示例
---
## `search`
- 搜索镜像源里可下载的镜像
- 不被国内镜像加速器所代理或加速, 因此客户端会直接尝试访问海外的DockerHub, 因此不推荐使用
- 建议直接从镜像网站搜索需要的镜像
### 参数
### 示例
- 搜索镜像
	- `docker search ubuntu`
---
## `image`
### 参数
- `ls`: 查看所有镜像
## `images`
### 参数
- `--all`: 查看所有镜像
---
1. 配置docker网络模式，比如桥接，host等
2. 查看容器的配置
	1. 所有配置

		1. docker inspect //查看所有配置
		2. docker inspect --type container

	2. 单一配置

	3. 加上 --format '{{.Config.Cmd}}'

3. 查看某个docker网络有哪些容器在使用

	1. docker network inspect

4. 查看docker网络信息

	1. docker network ls：显示网络id及其网络模式

5. 查看所有容器

	1. docker ps -a

6. 查看运行中的容器

	1. docker ps

7. 删除容器

	1. docker rm <容器名> //删除之后要创建通过docker run

8. 清理未使用的资源

	1. docker system prune -fa：删除关闭的容器，未使用的数据卷和网络，以及无标签的镜像

9. 启动/停止容器（容器名可通过docker ps查看）

	1. docker start <容器名>
	2. docker stop <容器名>

10. 拷贝文件到某个容器的环境中

	1. docker container cp <本地系统文件路径> <容器名：容器环境路径>

11. 进入到容器环境

	1. 根据容器使用的环境是sh还是bash

		1. docker exec -it /bin/bash
		2. docker exec -it /bin/sh

	4. docker attach <container_name_or_id>
	5. attach和exec的区别，attach是进入当前会话，exec是创建一个新的会话

12. 重启容器

	1. docker restart

13. 查看由Supervisor管理的所有进程的状态

	1. docker exec pmon supervisorctl status

14. 查看所有镜像

	1. docker images --all：显示所有镜像

15. 基于基础镜像构建一个新的镜像：标签

	1. docker build：基于Dockerfile文件构建一个新的镜像
		1. 参数

			1. -t ：为构建的镜像指定一个标签

16. 删除镜像

	1. docker rmi <镜像ID或镜像名称>：删除指定镜像
	2. docker image prune -a：删除所有未使用的镜像
	3. 删除none repository和none tag镜像

17. 查看镜像依赖

	1. docker history

18. 从镜像创建容器

	1. user@host:~$ docker run -it -v ${HOME}/src:/home/build/src --name onie debian:build-env
	2. 参数解析

		1. -v挂载一个主机目录或文件到容器，<主机目录>:<容器目录>
		2. --name：为容器指定一个名称
		3. debian:build-env
		
			1. debian是镜像名
			2. build-env是基于这个镜像的一个预配置标签

19. 离线传递

	1. docker save

		1. 示例：docker save -o debian_buster.tar debian:buster

	3. docker load

		1. 示例：docker load -i debian_buster.tar