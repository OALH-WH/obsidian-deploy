---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/网元常见操作/product源码剖析/","dg-note-properties":{}}
---

- 从product_main.c：

	- parse_opts函数：

		- 解析执行参数

			- ...

			- s

				- get_slot_id

					- init_glue_firmware

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/%E5%85%AC%E5%8F%B8/sino/%E7%BD%91%E5%85%83%E5%B8%B8%E8%A7%81%E6%93%8D%E4%BD%9C/images/WEBRESOURCE0d3ca423780512e25d4729dfb25b6158image.png)

						- init_card_info

							- get_card_type

					- get_slot_idinternal

					- uninit_glue_firmware

			- h

				- set_watchdog

- 板卡组信息定义在product_interface.c::gCardGroupinfo

- 各个板卡IO接口定义在product_interface.c: gBaseIOInfo