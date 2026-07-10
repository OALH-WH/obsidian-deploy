---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/AONOS/北向 or CLI获取数据 or 配置流程/","dg-note-properties":{}}
---

1. 北向 and CLI代码库：sonic-mgmt-common and sonic-mgmt-framer and sonic-utiles

1. 北向

1. 编译

1. d4os根目录下执行CROSS_BLDENV=1 KEEP_SLAVE_ON=1 SLAVE_PORT=22000 make target/debs/buster/sonic-mgmt-framework_1.0-01_arm64.deb-rebuild

1. cd src/sonic-mgmt-framer

1. source build_env && make rest-server

1. 替换

1. 进入framer的docker容器中，ps查看rest-server进程启动参数信息

1. supervisorctl关闭进程，并前端执行编译好的rest-server

1. CLI

1. 编译：？