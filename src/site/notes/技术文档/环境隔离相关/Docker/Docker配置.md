---
{"dg-publish":true,"permalink":"/技术文档/环境隔离相关/Docker/Docker配置/","dg-note-properties":{}}
---

# 常见配置
## Dockerfile
- 构建docker镜像
### 常见问题
#### DNS没配置, 导致构建过程中域名解析失败
### 构建配置
- 构建配置中, 指令每执行一次就会在docker上新建一层, 所以过多无意义的层, 会导致镜像膨胀过大
- 当某一层指令被改变时, 前面的层如果存在缓存可以直接使用缓存快速构建
	- 而后面的所有层缓存都会失效, 因此经常变动的指令应该放在后面
- 重新构建不需要先删除镜像, 可执行重复执行构建命令
- 构建配置中不能执行运行态的内容, 比如服务不能后台运行, 否则要么无效(RUN server), 要么容器直接退出(CMD/ENTRYPOINT ...)
#### 指令
- `ENV <environment_var>=<value>`: 指定环境变量, 在构建阶段和运行阶段都起作用
- `ARG <environment_var>`: 声明环境变量, 只在构建阶段起作用, 需要在执行构建命令时定义
- `COPY <local_host_path: 上下文路径> <container_path>`: 复制主机目录/文件到镜像
	- 示例
		- `eg. COPY ./STM32MP157Mini/cross_compiler_tools_chain/gcc-arm-9.2-2019.12-x86_64-arm-none-linux-gnueabihf /opt/toolchain/`: 会把指定目录下的内容以及目录结构复制到 `/opt/toolchain/`目录下, 参考[[技术文档/Linux/linux常用操作/文件系统相关/文件_目录相关/cp命令\|cp命令]]
- `FROM <镜像名称[:镜像标签]>`: 指定基础镜像
	- 可通过镜像源网站查看
	- 常见基础镜像名称
		- `hello-world`: 用来检测网络连通性
		- `debian`: debian系统镜像
			- `tag`
				- `latest`: 最新版
				- `bookworm-slim`: 稳定版(最常用)
				- `trixie`: 测试版
- `RUN <commands>`: 执行命令
	- 一般用来包管理命令下载环境依赖
- `CMD <["CMDPATH", "ARGUMENTS"]>`: 用于指定容器的启动位置, 比如在某个命令执行之后, 相当于把启动命令之后的状态也存入镜像
- `ENTRYPOINT <["CMDPATH"]>`: 用于指定容器的启动位置, 比如需要在启动容器之前做某些配置, 启动某些程序, `CMD`的进阶版操作, 常配合`COPY`使用
#### 示例
- 注意
	- apt-get安装依赖必须要加-y参数, 否则构建必定失败, 参考[[技术文档/Linux/linux常用操作/软件包管理/apt包管理/使用\|使用]]
```dockerfile
# Dockerfile.buildroot-minimal
FROM debian:latest
RUN apt-get update && apt-get install -y --no-install-recommends depend1 \
depend2 \
depend3 \
... \
# 清理apt-get update之后的软件包缓存信息, 减少存储空间的占用
rm -rf /var/lib/apt/lists/*
```
---
## 使用docker容器, 创建启动脚本
---
## 启动docker服务和设置开机自启
```
sudo systemctl enable docker
sudo systemctl restart docker
```
---
## 建立docker用户组
- 默认情况下, docker命令会使用docker的Unix socket和docker引擎通信, 而只有root用户和docker组的用户才可以访问docker引擎的Unix socket
```shell
sudo groupadd docker
sudo usermod -aG docker $USER # 把当前用户加入docker组
```
### 常见问题
#### 添加到了docker组还是无法使用docker命令连接到服务
```shell
# 检查docker.sock的权限和所属组, 如果不对可能要修改
ls -l /var/run/docker.sock

# 修改用户/组权限信息要重新登录才能生效
用su命令重新登陆, eg. su wuhang
```
---
## 镜像源配置
- `/etc/docker/daemon.json`
	- 如果文件不存在, 直接创建即可
### 示例
#### 网络代理配置
```json
{
	"proxies": {
		"http-proxy": "",
		"https-proxy": "",
		"no-proxy": ""
	}
}
```
#### 添加镜像加速器地址  
```json
{
  "registry-mirrors": [
  "https://docker.xuanyuan.me"
],
  "insecure-registries": [
  "docker.xuanyuan.me"
],
  "dns": ["119.29.29.29", "114.114.114.114"]
}
```