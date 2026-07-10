---
{"dg-publish":true,"permalink":"/技术文档/z_不维护_单片机/ARM架构单片机/基础知识/内核知识/SCB（system control block，系统控制块）/","dg-note-properties":{}}
---

1. SCB（SCB，System Control Block，系统控制块）

1. CPUID：CPU ID

1. 作用：CPUID基地址寄存器，包含处理器型号、版本等相关信息，是只读的。

1. ICSR（interrupt Control and State Register）：中断控制和状态寄存器

1. 作用：用于设置和清除系统异常的挂起状态，以及确定当前执行的异常/中断编号

1. VTOR（vector table off register）：向量表偏移寄存器

1. 作用：存储要使用的向量表的地址

1. AIRCR（Application interrupt and Reset Control Register）:应用中断和复位控制寄存器

1. 作用：用于请求系统复位，识别系统的大小端，以及清除所有异常活动状态

1. SCR（System Control Register）：系统控制寄存器

1. 作用：控制进入和退出低功耗状态的特性

1. CCR（Cofniguration Control Register）：配置控制寄存器

1. 作用：指示Cortex-M处理器行为的某些方面，如除数为零和未对齐内存访问是否触发用法

1. SHP（System Handler Priority Register）：系统处理程序优先级寄存器

1. 作用：设置具有可配置优先级的异常处理程序的优先级级别

1. SHCSR（System Handler Control and State Register）：系统处理控制和状态寄存器

1. 作用：用于屏蔽异常和中断