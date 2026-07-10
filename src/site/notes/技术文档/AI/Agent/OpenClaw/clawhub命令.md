---
{"dg-publish":true,"permalink":"/技术文档/AI/Agent/OpenClaw/clawhub命令/","dg-note-properties":{}}
---

# 下载安装
- `npm install -g clawhub`
# clawhub子命令
## 位置参数
- `update`
- `search <key str>`
- `install <skill name>`
- `uninstall <skill name>`
- `publish <skill path> --version <VER, eg. 1.0.0>`
- `delete <skill name>`: 从开源远程仓库中删除这个`skill`
## 可选参数
- `--dir <skill install directory>`: 指定skill安装路径
	- `~/.agents/skills/`: 通用`skill`全局目录