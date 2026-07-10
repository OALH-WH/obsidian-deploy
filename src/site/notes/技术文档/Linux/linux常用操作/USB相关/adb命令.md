---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/USB相关/adb命令/","dg-note-properties":{}}
---

# 背景
- 全称`android debug bridge`
- `C/S`架构, 服务端运行在设备上, 客户端运行在开发宿主机上
# Client
## 安装
## 命令参数
### `devices`
- 检测连接的设备 
- 如果为`unauthorized`, 则表示未经授权, 无法访问
### `root`
- 切换到`root`权限
### `shell [<COMMAND>]`
- 进入`shell`
- `or`执行`shell`命令
## 常见问题
### 设备检测为`unauthorized`
#### 解决方案1(调试Android手机)
- `adb kill-server`
- `adb start-server`
- 重新拔插`USB`
# Server
## 安装
## 配置