---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/网络相关/抓包软件/tcpdump笔记/","dg-note-properties":{}}
---

- 抓包实例

	- 

- 在 tcpdump 的世界里，过滤器的实现，都是通过一个又一个的参数组合起来，一个参数不够精准，那就再加一个，直到我们能过滤掉无用的数据包，只留下我们感兴趣的数据包。

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/linux%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C/%E7%BD%91%E7%BB%9C%E7%9B%B8%E5%85%B3/images/WEBRESOURCEd8bf4e104c2452c0b36426b387569b57image.png)

- 抓取http报文

	- tcpdump -i eth1 -s  0 -A

- 