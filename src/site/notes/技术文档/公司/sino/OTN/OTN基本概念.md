---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/OTN/OTN基本概念/","dg-note-properties":{}}
---

OTN光传送网=DWDM（dense wavelength division mutiple，密波）+SDH（synchronous digital hierarchy，同步数字体系）

WDM（波分复用）：分为CWDM（粗波）和DWDM（密波）

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEe5eb19930c43e101f22e7ab698001499image.png)

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEd16e4a94e3c4ceba5acec6dccdede9a1image.png)

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEc9da05b107682f690ca0b2abb9a5d63cimage.png)

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCE291d864bb829bc4ddb26b743c4ebeb89image.png)

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCE469dbad0530c581cceb4a70493eea6cdimage.png)

- OTN帧分为三部分组成

1. 用于运行、维护、管理的开销区

1. 用于承载用户数据的净荷区

1. G.709帧里包含的向前纠错FEC区（使用的是RS码）（G.709新增的）

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCE15472e650d53fa56d2af0855ee03016fimage.png)

- OTN帧中各个区域的列数

	- OTN尺寸和OTUk信号的k无关，帧尺寸都是4*4080个字节，但不同等级速率也就是k不同，信号帧的周期是不同的

	- 总结：信号速率=(每帧字节数*帧数)/s

	- 数据在传输过程中，是从上到下，从左到右进行填充传输

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCE9a9d461090e8cf19e390a05e3f8c16d1image.png)

- OTN的开销：

	- 电层开销

		- 开销区由四部分组成

			- 帧定位、OTU开销、ODU开销、OPU开销

			- 位置

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCE05e42288aaa993712db15b42c78e9552image.png)

	- 光层开销

		- OTSN（光传送段开销）

		- OMSN（光复用段开销）

		- OCHN（光通道段开销）

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/OTN/images/WEBRESOURCEb0f66a7b48feb8bcca021f677076e86fimage.png)