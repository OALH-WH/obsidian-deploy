---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/编译工具链相关/工具链/调试器的使用/调试实例/单片机调试/调试服务器/openocd软件/","dg-note-properties":{}}
---

# 下载_安装
# 配置
## interface
# 参数

# 实例
---
1. 目录解析

2. share

3. openocd/scripts

4. interface

5. 调试适配器, 例如ST-Link

6. targfet

7. 目标板

8. 常用参数

9. -f //可以多次使用, 指定多个配置文件

10. -c //后跟下载命令, 需要你提供你开发板的文件地址以及下载偏移

11. 示例

12. eg. openocd -f interface/stlink.cfg -f target/stm32h7x.cfg -c "program demo.bin exit reset"