---
{"dg-publish":true,"permalink":"/技术文档/芯片/指令集架构/ARM架构/z_不维护/ARM架构与汇编指令/","dg-note-properties":{}}
---

1. C/C++中嵌套汇编

1. GNU C内联汇编风格（比如arm-none-eabi-gcc）

1. 注意

1. 不接受三立即数的写法

1. 格式

1. __asm__ volatile ("汇编指令" : 输出约束 : 输入约束 : 可能修改的寄存器);

1. 解析

1. 输出约束

1. 告诉编译器哪些c变量会被修改

1. 输入约束

1. 告诉编译器哪些C变量会被用到

1. 修改寄存器

1. 高速编译器哪些寄存器可能被我动过（避免编译器优化错误）

1. 约束字符

1. =r：输出到寄存器，并写回变量

1. r：输入到任意通用寄存器

1. 0：和第零个操作数使用同一个寄存器

1. a：指定寄存器，arm中不合法

1. 实例

```cpp
int foo() {
    int val;
    __asm__ volatile ("mov %0, #42" : "=r"(val));
    return val;  // 返回 42
}
//这里%0对应val，=r表示写到某个寄存器

int add5(int x) {
    int result;
    __asm__ volatile (
        "add %0, %1, #5"
        : "=r"(result)      // 输出
        : "r"(x)            // 输入
    );
    return result;
}
//这里%0对应result，%1对应x，r表示把变量x的值存入某个寄存器

void test() {
    int a = 3, b = 4, res;
    __asm__ volatile (
        "add %0, %1, %2\n\t"
        "lsl %0, %0, #1"
        : "=r"(res)
        : "r"(a), "r"(b)
    );
    // res = (a+b) << 1
}
//多行汇编
```

1. ARMCC/keil风格（比如keil IAR等商用软件）

1. 实例

1. 独立汇编函数

```cpp
__asm int add_two(int a, int b) {
    ADD r0, r0, r1   ; r0 = r0 + r1
    BX  lr           ; return
}

```

1. 函数中嵌入汇编代码段

```cpp
void foo() {
    int x = 10;
    __asm {
        MOV r0, #5
        ADD r0, r0, x
    }
}

```

1. 常用汇编指令

- 标号（一般）：__initial_sp只是一个**标号**，标号主要用于表示一片内存空间的某个位置，等价于C语言中的“地址”概念。地址仅仅表示存储空间的位置。

- 立即数

	- =0x8000000

		- GNU as 的伪指令

		- 含义

			- 如果常量能直接编码，就翻译成mov r0， #0x80000000

			- 如果常量太大，就在代码附近生成一个字面量，然后用ldr r0, [pc,...]来加载 //只适用于ldr指令

	- #5

		- 只能加载（8位+偶数位旋转），如果常量太大会报错

		- 循环左移n位，等于右旋（32-n位）//循环左移即把最右边的值移到最左边

- 伪指令:一般以.开头

	- EQU/.equ（equal）：定义常量

	- .：表示当前正在执行的地址

		- 例如B     .:表示无条件跳转到当前地址，形成了一个死循环

	- .data：开始数据段，指示后面的内容是数据而非代码

	- .text：开始代码段，指示后面的内容是可执行代码

	- .global：声明全局符号，使其可以在其他模块中访问

	- .section：用于定义代码或数据的段，控制链接器如何处理这些段

	- .align：用于设置数据的对齐方式，以确保在内存中按照特定边界对齐。

	- .macro：定义宏，可以在代码中多次调用以简化代码

	- .word：通常用于在数据段中定义一个或者多个字大小的存储单元，一个字的大小一般为4个字节（本身不会分配空间，而是把这个标号表示的地址存放到当前内存位置，标号实际代表的首地址一般是在链接脚本中指定）

	- .weak：表示该标号可以在其他地方重定义，即声明一个弱符号（weak signal），可以在其他地方声明强符号（strong signal），在处理弱符号和强符号时会优先使用强符号

		- 疑问：弱符号和弱符号？

	- .type <Reset_Handler>, %function：表示把复位处理声明为函数

- 其他指令

	- AREA：表示定义一个代码或者数据段

		- 属性

			- stack：段名

			- noinit：表示此数据段不需要填入初始数据

			- readwrite：可读可写

			- align=3：表示首地址按照2^3对齐

	- SPACE：给指定段分配栈空间

	- PRESERVE8:指定当前文件保持八字节对齐

	- EXPORT：将标号声明为可被外部引用

	- DCD：表示分配1个4字节的空间，类似于定义变量

	- PROC...ENDP：表示程序的开始和结束

	- WEAK声明：说明我们在外部可以自定义复位中断处理函数

	- IMPORT：告知要使用的标号在其他源文件定义

- 传送指令

	- MOV

		- 实例

			- mov LR, PC //将PC寄存器的值赋值到LR寄存器中

			- mov r0, #5 //给r0赋值为5

	- MOVS

		- 实例

			- 

- 寄存器入栈出栈指令

	- PUSH

	- POP

- 加载存储指令

	- MSR（Move to Status Register）：用来把数据从立即数或者通用寄存器写到状态寄存器中，在ARM架构中通常用来对程序状态寄存器进行读写操作，如CPSP和SPSP，还可以对控制寄存器，如MSP，PSP进行操作

	- LDR(loader)

		- 实例

			- ldr r3, =_sidata //表示将_sidata代表的数据（值or地址）放入r3寄存器

			- ldr r3, [r3, r1] //表示将r3+r1得到的指针指向的地址上存储的值加载到r3寄存器

	- STR(store)

		- 实例

			- str r3, [r0, r1] //表示将r3上存放的数据（值or地址）存储到r0+r1得到的指针指向的地址上

- 跳转指令

	- BL(branch and link)

		- 跳转到指定地址

		- 记录返回地址，返回地址保存在R14(lr)中

	- BX（Branch and Exchange）：跳转到指定地址根据最低位来选择跳转模式

		- 如果目标地址最低位为0，则进入ARM模式

		- 否则进入Thumb模式（16位指令集）

	- BLX（Branch with Link and Exchange）：跳转到指定地址根据最低位来选择跳转模式，并且记录返回地址

		- 跳转条件上同

	- B

		- 跳转到指定地址

- 运算指令

	- ADDS（Add with Update）

		- 格式：adds r1, r2, r3

		- 作用：将r2和r3的值相加，并且把结果存储到r1中，同时更新标志位

		- 详解：adds是add的变体，其中的s表示在执行加法后更新条件标志（如零标志 Z（zero）、负标志 N（negative）、溢出标志 V（overflow） 和进位标志 C（carry））

			- 如果结果是负数则N标志设为1

			- 如果结果为零，则Z标志设为1

			- 如果发生进位，则C标志设为1

			- 如果结果溢出，则V标志设为1

	- cmp

		- 格式：cmp r2, r3

		- 作用：比较r2和r3，结果通过更新标志位来反映

		- 详解

			- 如果r2-r3为负数，则N置为1

			- 如果r2-r3结果为零，则Z置为1

			- 如果r2-r3为负数，即产生了借位，则C置为0

			- 如果计算中发生了溢出，则V置为1

	- bcc（branch if carry clear， 如果C标志位清零则跳转）

		- 格式：bcc CopyDataInit

		- 作用：当C标志位为零就跳转到CopyDataInit标号

- 指令后缀

	- b：表示这个指令占1个字节

	- h：表示这个指令占2个字节

	- r：表示这个指令占4个字节

	- 不加后缀：默认占4个字节

-  CPU内部常用寄存器共15个

	- r12（FP）

	- r13（SP）

	- r14（LR）

	- r15(PC)

- 栈的进出

	- push从高地址到低地址

	- pop从低地址到高地址

1. 实例

1. 函数调用

```cpp
/*test1.c*/
#include <stdio.h>

int foo1(int m,int n,int p)
{
        int x = m + n + p;
        return x;
}
 
int main(int argc,char** argv)
{
        int x,y,z,result;
        x=11;
        y=22;
        z=33;
        result = foo1(x,y,z);
        printf("result=%d\n",result);
        return 0;
}

//arm assembly
//省略不相关代码
0000826c <foo1>:
    826c:    e52db004     push    {fp}        ; (str fp, [sp, #-4]!)
    8270:    e28db000     add    fp, sp, #0
    8274:    e24dd01c     sub    sp, sp, #28
    8278:    e50b0010     str    r0, [fp, #-16]
    827c:    e50b1014     str    r1, [fp, #-20]
    8280:    e50b2018     str    r2, [fp, #-24]
    8284:    e51b2010     ldr    r2, [fp, #-16]
    8288:    e51b3014     ldr    r3, [fp, #-20]
    828c:    e0822003     add    r2, r2, r3
    8290:    e51b3018     ldr    r3, [fp, #-24]
    8294:    e0823003     add    r3, r2, r3
    8298:    e50b3008     str    r3, [fp, #-8]
    829c:    e51b3008     ldr    r3, [fp, #-8]
    82a0:    e1a00003     mov    r0, r3
    82a4:    e28bd000     add    sp, fp, #0
    82a8:    e8bd0800     pop    {fp}
    82ac:    e12fff1e     bx    lr

000082b0 <main>:
    82b0:    e92d4800     push    {fp, lr}
    82b4:    e28db004     add    fp, sp, #4
    82b8:    e24dd010     sub    sp, sp, #16
    82bc:    e3a0300b     mov    r3, #11
    82c0:    e50b3014     str    r3, [fp, #-20]
    82c4:    e3a03016     mov    r3, #22
    82c8:    e50b3010     str    r3, [fp, #-16]
    82cc:    e3a03021     mov    r3, #33    ; 0x21
    82d0:    e50b300c     str    r3, [fp, #-12]
    82d4:    e51b0014     ldr    r0, [fp, #-20]
    82d8:    e51b1010     ldr    r1, [fp, #-16]
    82dc:    e51b200c     ldr    r2, [fp, #-12]
    82e0:    ebffffe1     bl    826c <foo1>
    82e4:    e1a03000     mov    r3, r0
    82e8:    e50b3008     str    r3, [fp, #-8]
    82ec:    e59f301c     ldr    r3, [pc, #28]    ; 8310 <main+0x60>
    82f0:    e1a00003     mov    r0, r3
    82f4:    e51b1008     ldr    r1, [fp, #-8]
    82f8:    eb000347     bl    901c <_IO_printf>
    82fc:    e59f0010     ldr    r0, [pc, #16]    ; 8314 <main+0x64>
    8300:    eb000354     bl    9058 <_IO_puts>
    8304:    e24bd004     sub    sp, fp, #4
    8308:    e8bd4800     pop    {fp, lr}
    830c:    e12fff1e     bx    lr
    8310:    00063214     andeq    r3, r6, r4, lsl r2
    8314:    00063220     andeq    r3, r6, r0, lsr #4
//省略不相关代码
```