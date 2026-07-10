---
{"dg-publish":true,"permalink":"/技术文档/公司/sino/电层/pla层/","dg-note-properties":{}}
---

1. pla层里有各个光模块的配置函数和获取函数和各个模块寄存器地址

	- 每种模块的底层实现的文件名可以通过pla cfp module定义的模块类别中的第一个成员变量名确定

	- pla cfp module:可以查看模块的PN（料号）

	- pla hash:可以查看对应模块的寄存器地址

- 全局变量

	- pPlaCardData

		- get_port_present（从pla cfp init.c: PLA_RegisterCfpIO获取，实际函数为）

		- get_port_preent_change：上同

		- aval_cfp_port_mask：板卡上线路侧模块端口位置掩码（从pla cfp init.c: PLA_InitMoudle函数获取）

	- pla cfp fun.c: gPlaCfpFunInfo: 线路侧模块相关函数结构体

	- gpPlaCfpPortData

		- bReady:

		- cfp_config：配置结构体

		- cfp_runinfo：获取当前配置结构体

			- sCfpParam：光模块当前配置结构体（数据获取从每种模块的底层实现的源文件中拿）

				- nType: 从pla cfp init.c: pla_get_cfp_type函数中获取

				- sVendorName: 上同

				- sVendorPartNumber：上同

				- sVendorSerialNumber：上同

		- pcfp_func: 从gPlaCfpFunInfo结构体中获取对应模块的polling函数（pla cfp init.c: pla_cfp_polling_task）

	- pPlaCardData

		- cardIo:注册了寄存器访问接口

			- 注册函数为pla_cfp_init.c: PLA_RegisterCfpIO()