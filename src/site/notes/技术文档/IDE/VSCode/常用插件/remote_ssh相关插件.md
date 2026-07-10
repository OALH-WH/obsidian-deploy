---
{"dg-publish":true,"permalink":"/技术文档/IDE/VSCode/常用插件/remote_ssh相关插件/","dg-note-properties":{}}
---

# Remote-SSH
## 常见实例
### 离线安装vscode-server
- 内网环境下, `vscode`无法直接从外网下载`vscode-server`, 只能手动在外网环境中去下载
#### 步骤
1. 手动下载`vscode-server`, 参考[[技术文档/IDE/VSCode/常用插件/remote_ssh相关插件#离线安装vscode-server\|#离线安装vscode-server]]
2. 压缩包解压到指定设备的`~/.vscode-server/bin/<COMMIT NUM>/`目录下面
##### 最终现象
![Pasted image 20260414164854.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/IDE/VSCode/%E5%B8%B8%E7%94%A8%E6%8F%92%E4%BB%B6/resources/Pasted%20image%2020260414164854.png)
#### vscode-server下载网址
- <https://update.code.visualstudio.com/commit:xxx/server-linux-x64/stable>
	- `commit:xxx`: `xxx`需要替换为`vscode`实际Commit号, 参考[[技术文档/IDE/VSCode/常用设置/查看vscode软件信息\|查看vscode软件信息]]