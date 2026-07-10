---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/SONIC/AONOS/南向内容/LAI（redis建模）/","dg-note-properties":{}}
---

1. 目录：LAI

1. 生成的目标文件：LAI/meta/laimetadata.c

1. 实例

1. linecard增加一个属性

1. lailinecard.h中增加一个属性，定义其类型以及访问权限

1. 编译

1. 进入liblairedis或者liblaisino的容器

1. cd src/sonic-lairedis/LAI/meta

1. make

1. device/alibaba/<主控类型>/<板卡类型>/flexcounter.json.j2添加对应属性git

1. 目的：syncd会调用lai接口采集这里指定的属性

1. 编译对应的包

1. 命令：CROSS_BLDENV=1 make target/debs/buster/obx2000_1.0.0_all.deb-rebuild