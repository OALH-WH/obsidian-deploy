---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/AONOS/device板卡初始化DB配置文件/","dg-note-properties":{}}
---

1. 路径

1. device/alibaba/arm64-obx2000-r0

1. 原理

1. 根据j2文件自动生成模板

1. 编译

1. CROSS_BLDENV=1 make target/debs/buster/obx2000_1.0.0_all.deb-rebuild

1. 替换

1. 编译之后会在对应板卡类型下生成受支持槽道的DB配置文件

1. 把这些文件替换到设备上/etc/sonic/factory/下对应板卡类型的配置文件

1. 重启orchagent

1. 不用这种方式了，重新配置板卡类型（依赖：板卡不在位）可以通过sith jrpc force_not_present linecard 3 1命令在不需要插拔板卡的情况下强制把板卡在位信息置为不在位

1. 