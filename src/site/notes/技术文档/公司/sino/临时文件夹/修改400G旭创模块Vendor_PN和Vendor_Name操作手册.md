---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/临时文件夹/修改400G旭创模块Vendor_PN和Vendor_Name操作手册/","dg-note-properties":{}}
---

1.  环境搭建

1. 使用SecureCRT远程终端连接软件进入网元

1. 注意：Vendor_PN和Vendor_Name可通过网元操作（gettable plug命令读到的VendorPN和VendorName字段下的值就是对应槽道端口上模块的Vendor_PN和Vendor_Name信息）获取

1. T4QH板卡 + 400G旭创模块（Vendor_Name：INNOLIGHT，Vendor_PN: CT-CTS400SLHPA00）

1. 主控上通过lt 槽道号，进入线卡管理界面，账号密码皆为admin

1. 例如，lt 1：进入槽道1的T4QH板卡管理界面

1. 点击SecureCRT的Script->Run, 进入文件选择界面，选择给定的脚本文件，等待执行结束

1. 执行logout命令，回到主控

1. 执行tools_set reboot_slot 槽道号 warm，热起线卡

1. 等待线卡重启，重新获取模块Vendor_PN和Vendor_Name

1. 操作步骤截图如下

1. 进入线卡

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE81a7828f8219a01298ae06f3ef44bc61image.png)

1. 执行脚本文件

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE2ec0d4f9c4854df006f55b25cac9b1baimage.png)

1. 等待最后一条命令执行结束之后，执行logout命令退出线卡

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE3e95da8384cebb5acbb6d2ac1467f259image.png)

1. 执行tools_set reboot_slot 2 warm命令，热起线卡

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCEa52144f9afedd1a7934b9be6628ddedeimage.png)

1. 执行gettable plug命令，获取到的值为10.600.6505和XN即为成功，换下一个模块重复以上操作即可

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE997a77d85422b7cb1ad8490b0e6b6d77image.png)