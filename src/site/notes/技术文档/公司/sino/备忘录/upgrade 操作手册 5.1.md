---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/备忘录/upgrade 操作手册 5.1/","dg-note-properties":{}}
---

# 模块升级步骤
## 1. 连接主控

## 1.1 IP已经配好, 使用ssh网络连接主控
- 这里用`windterm`终端软件做演示
- 先建立会话
![Pasted image 20260108182147.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108182147.png)
![Pasted image 20260108182257.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108182257.png)
- 输入账号密码进入主控
![Pasted image 20260108182331.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108182331.png)
## 1.2 没有配主控IP, 使用主控eth1网口和电脑直连
- 没有配置管理ip的情况下，主控自带一个默认ip， `192.168.126.1/30`
- 需要配置电脑上的**和主控网口用网线相连的以太网卡上的IP**(保持和主控网口IP是同一个网段) `eg. 192.168.126.2`
	- 比如win11电脑找到对应以太网卡的IP分配
		- ![Pasted image 20260109102806.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260109102806.png)
	- 如下图所示配置IP并保存
		- ![Pasted image 20260109103438.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260109103438.png)
- 然后参考第1.1的步骤操作, 只是把**要连接的主机IP换成 `192.168.126.1`**
	- ![Pasted image 20260109102639.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260109102639.png)
## 2. 从主控登录到要实现升级模块操作的线卡
- 首先执行`mt 3`进入3槽升级卡, 升级卡是几槽就`mt`到几槽
![Pasted image 20260108182529.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108182529.png)
## 3. 执行升级命令
- 执行命令 `/app/upgrade.sh` or `/app/upgrade.sh [your fw version]` `eg. /app/upgrade.sh 1.77.7`
- 命令执行后，返回的提示信息的最后一行带有日志文件的位置, `eg. /app/upgrade_record/upgrade_2026-01-08_19:20:10_PN_10.600.6508_SN_X423390029_no_file.log`
- 没有真正升级的几种情况
	- 第一个命令是没有参数, 即升级为默认版本1.66.6, 但是当前版本已经是1.66.6, 因此不会升级
	- 第二个命令是指定了自定义的固件版本, 会去 `/app/`找固件升级文件`400G_v1.77.7.bin`, 没找到则输出没有这个文件
![Pasted image 20260108184715.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108184715.png)
- 正在更新固件版本情况如下
![Pasted image 20260108200136.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108200136.png)
![Pasted image 20260108192734.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108192734.png)
- 成功执行的情况如下
	- 不加参数, 默认升级到1.66.6版本, 会校验当前固件版本, 如果小于1.66.6才会升级, 如下图所示
		- ![Pasted image 20260108195553.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108195553.png)
	- 带指定版本参数, 不做校验, 只要固件版本文件存在, 直接升级到指定版本(主要做降级使用), 如下图所示
		- ...

## 4. 查看返回结果并打包所有日志
- 根据脚本的输出查看本次升级日志的输出结果
	- 没有实际升级成功的日志结果
		- ![Pasted image 20260108184849.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108184849.png)
	- 实际升级成功的日志截图
		- ![Pasted image 20260108195451.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108195451.png)
- 打包日志, 在升级卡中, 执行命令
	- `tar -czvf /tmp/upgrade_record.tar.gz /app/upgrade_record/upgrade_*.log`
	![Pasted image 20260108192449.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108192449.png)
## 5. 退出登录到主控
- 其中第1/2步, 如果没有执行过第5步, 或者断开了, 可以不用执行1/2步
![Pasted image 20260108190016.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108190016.png)
## 6. 上传本次升级日志到主控
- 命令如下
	- `ftpget -u root -p sino-telecom 172.16.200.3 /tmp/upgrade_record.tar.gz /tmp/upgrade_record.tar.gz`
		- 命令中的 `172.16.200.3`表示3槽升级卡, 如果是其他槽位请用 `172.16.200.<实际槽位号>` `eg. 172.16.200.7`表示从槽道7获取打包好的日志
![Pasted image 20260108191216.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108191216.png)
## 7. 从主控把日志下载到本地电脑
- 这里示例使用`winscp`软件把主控日志下载到本地电脑
- 先登录主控
- ![Pasted image 20260108191948.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108191948.png)
- 再找到主控`tmp`目录下打包好的文件拖拽到本地目录, 我这里本地目录使用`Downloads`目录
- ![Pasted image 20260108192144.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E5%A4%87%E5%BF%98%E5%BD%95/resources/Pasted%20image%2020260108192144.png)