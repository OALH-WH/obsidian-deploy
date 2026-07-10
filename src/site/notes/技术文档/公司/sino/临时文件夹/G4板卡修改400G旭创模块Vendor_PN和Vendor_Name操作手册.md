---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/临时文件夹/G4板卡修改400G旭创模块Vendor_PN和Vendor_Name操作手册/","dg-note-properties":{}}
---

1. 环境搭建

1. 使用任意远程终端控制软件进入网元

1. M20DHE板卡+400G旭创模块（Vendor_Name：INNOLIGHT，Vendor_PN: CT-CTS400SLHPA00）

1. 操作步骤

1. 上传.sh脚本文件到主控的/tmp目录

1. 使用scp命令传输脚本文件到线卡

1. 例如，scp /tmp/文件名 172.16.200.1:/tmp/, 传输脚本文件到槽道1的G4线卡的tmp目录下

1. 注意：线卡IP可以通过mt 槽道号命令的输出打印查看

1. 主控上通过mt 槽道号命令，进入G4线卡终端，并cd到tmp目录

1. 例如，mt 1，进入槽道1的G4线卡终端上，cd /tmp，进入tmp目录

1. 给脚本文件执行权限，执行chmod +x 脚本文件名命令

1. 例如，chmod +x G4_Script.sh

1. 执行脚本并热起

1. 例如，./G4_Script.sh，执行脚本，reboot，热起线卡

1. 回车返回到主控，执行gettable plug命令，查看是否PN和Vendor_Name更改为10.600.6505和XN

1. 操作步骤截图

1. 上传文件到主控tmp目录（推荐使用winscp）

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE3741295523c6f2472f6470b2d88d80a4image.png)

1. 从主控的tmp目录上传文件到线卡，密码同远程连接主控密码一样

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE38a9e9d081101f2b25ab76a01b99977fimage.png)

1. 进入线卡终端并进入tmp目录下

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE091124f4893422f6d59673d710a72dfaimage.png)

1. 给脚本文件执行权限，并执行脚本

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCEe69ca0d0d8f9a251df2f067530c95de3image.png)

1. 热起线卡

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE66d3330814f6c258e244dafb895dafb3image.png)

1. 查看是否更改成功

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E4%B8%B4%E6%97%B6%E6%96%87%E4%BB%B6%E5%A4%B9/images/WEBRESOURCE902119bfa884f8df98b4faba9f9a40ceimage.png)