---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文件系统相关/网络文件系统/NFS-Server/","dg-note-properties":{}}
---

# 安装
**软件包**
- `nfs-kernel-server | nfs-server`

**服务**
- `nfs-server.service | nfs-kernel-server.service`

**服务程序**
- `nfsdctl`
# 背景
- 一个网络文件系统服务, 可通过`mount`挂载网络文件系统, 参考[[技术文档/Linux/linux常用操作/文件系统相关/mount命令\|mount命令]]
# 依赖
## 内核配置
查看内核配置参考[[技术文档/Linux/常见目录和文件作用#**config.gz**\|常见目录和文件作用#**config.gz**]]或者[[技术文档/Linux/常见目录和文件作用#config-$(uname -r)\|常见目录和文件作用#config-$(uname -r)]]
- `CONFIG_NFSD_V2_ACL`: `nfs2`协议支持

# 配置
## `/etc/exports`
- **基本格式**: `<NFS PATH> <CLIENT IP>(<FLAGS>)`
	- `NFS PATH`: 可挂载的路径(服务所在机器上的路径)
		- 
	- `CLIENT IP`: 客户端IP
		- 可通过 `CIDR`描述来指定一个局域网, 参考[[技术文档/计算机网络相关/OSI七层模型/网络层/IP地址#`CIDR`(Classless Inter-Domain Routing, 无类别域间路由)表示法|CIDR]]
	- `FLAGS`
		- `rw`
		- `sync`
		- `no_subtree_check`: **不检查**父目录权限，可提升性能
		- `subtree_check`
		- `no_all_squash`: 不转变客户端用户(针对`root`用户)为匿名用户
		- `no_root_squash`: 不转变客户端用户(针对所有用户)为匿名用户
		- `anonuid=<UID>`: 设置匿名用户的`uid`
		- `anongid=<GID>`: 设置匿名用户的`gid`
# 实例
## window主机挂载/卸载Linux主机的路径
- `windows`风格 `mount`命令基本格式: `mount [-o options] [-u:username] [-p:<password | *>] <\\computername\sharename> <devicename | *>`
- `windows`风格 `umount`命令基本格式: `umount [-f] <-a | drive_letters | network_mounts>`
- 示例
	- `eg. mount \\192.168.1.200\home\kali\Projects\nfs_server_root_directory E:`
	- `eg. umount E:`
---
1. 问题实例

2. 客户端

3. 内核模块名

4. nfs.ko

5. 示例

6. 服务端

7. 服务名 //nfs-kernel-server为旧版

8. nfs-server

9. nfs-kernel-server

10. 注意

11. 内核配置项

12. CONFIG_NFSD_V2_ACL

13. =y

14. 表示如果系统支持NFSv2，那么它也支持ACL功能

15. 内核模块名

16. nfsd.ko

17. 实例

18. 查看内核是否启动了nfsd v2

19. 操作

20. eg. grep CONFIG_NFSD_V2 /boot/config-$(uname -r)

21. 注意

22. 如果没有这个配置项，说明内核不再支持nfsd v2

23. 查看运行中的服务器是否支持nfs v2协议

24. cat /proc/fs/nfsd/versions

25. 软件包

26. nfs-kernel-server

27. 查看内核是否启用指定版本

28. grep CONFIG_NFS_V2 /boot/config-$(uname -r)

29. 源码路径

30. fs/nfs

31. 模块名

32. fs/nfs/Makefile中有定义 //nfs.ko

33. 查看运行中的nfs服务器支持的版本

34. eg. cat /proc/fs/nfsd/versions

35. 查看nfs客户端支持的版本

36. eg. cat /proc/fs/nfs/version

37. 内核配置

38. 实例

39. nfsv2内核配置为module

40. modprobe nfsv2

41. 默认配置路径

42. **/etc/exports**

43. **作用**

44. **配置nfs根目录**

45. **实例**

46. **增加挂载nfs客户端root用户实际权限**

47. **eg. **/home/kali/Projects/test 192.168.1.3(rw,sync,no_subtree_check,no_root_squash)

48. **eg. **/home/kali/Projects/test 192.168.1.0/24(rw,sync,no_subtree_check)

49. /etc/nfs.conf

50. vers2=y: 增加支持版本

51. **/etc/default/nfs-kernel-server**

52. **PRCNFSDOPTS: 版本配置**

53. **示例**

54. **eg. **RPCNFSDOPTS="--nfs-

55. 测试

56. window创建一个nfs客户端,来mount nfs服务端指定的目录

57. 启用或关闭windows功能

58. NFS服务√

59. 管理工具√

60. 挂载

61. eg. mount.exe 192.168.1.100:/home/kali/Projects/test x:

62. 解析

63. 目的:把ip=192.168.1.5上的目录nfsroot挂载到x:

64. eg. umount x:

65. 解析

66. 目的:删除挂载目录

67. linux挂载nfs

68. eg. sudo mount -t nfs -o vers=4 192.168.1.100:/home/kali/Projects/test /mnt/nfs