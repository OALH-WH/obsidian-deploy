---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/定时任务相关/cron软件/","dg-note-properties":{}}
---

- crontab文件的含义：

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/linux%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C/images/WEBRESOURCEff514b197c3eecfa2bcf2306b92eed38image.png)

- 字段范围

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/linux%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C/images/WEBRESOURCEc172164a834bbf01b49a91607972bf98image.png)

```
星号（*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。
逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”
中杠（-）：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”
正斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如*/10，如果用在minute字段，表示每十分钟执行一次。
```