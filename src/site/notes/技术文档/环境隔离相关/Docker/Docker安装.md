---
{"dg-publish":true,"permalink":"/技术文档/环境隔离相关/Docker/Docker安装/","dg-note-properties":{}}
---

# 方式
## 脚本自动安装
```shell
curl -fsSL get.docker.com -o get-docker.sh # 可能拉取失败, 可以上官网看看
# 使用阿里云镜像安装
sudo sh get-docker.sh --mirror Aliyun
```
---
## apt包管理
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io
# kali
sudo apt-get install docker-compose docker.io
```
---
