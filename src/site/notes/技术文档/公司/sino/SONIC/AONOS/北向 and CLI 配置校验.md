---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/AONOS/北向 and CLI 配置校验/","dg-note-properties":{}}
---

1. 校验代码库：sith (有格式要求，要求使用clang-format格式)

1. 编译

1.  CROSS_BLDENV=1 make target/debs/buster/sith_0.0.1_arm64.deb-rebuild

1. 替换

1. ps 查看sith相关运行信息

1. 设备上systemctl stop sith

1. 手动前端执行编译好的sith