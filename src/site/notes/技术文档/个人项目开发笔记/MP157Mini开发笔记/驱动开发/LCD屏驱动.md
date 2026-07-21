---
{"dg-publish":true,"permalink":"/技术文档/个人项目开发笔记/MP157Mini开发笔记/驱动开发/LCD屏驱动/","dg-note-properties":{}}
---

# 驱动框架选型
参考[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/drm框架\|drm框架]]

## LCD屏硬件信息
**型号**
正点原子`ATK7016`屏, 即`RGB LCD`屏

**参数**
# 移植分析

包括下述工作
1. 设备树根节点提供`LCD`设备节点, 包含`backlight`引用和`ltdc`引用
	- `ltdc`全称`lcd-tft display controler`, 是片上外设, 驱动由芯片厂商负责编写, 用于通信控制
	- `drm`全称`display rendering manager`, 是外接模块, 驱动一般由模块厂商负责编写, 用于控制如何渲染屏幕
2. 在[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#platform_of_match变量\|panel-simple.c#platform_of_match变量]]中添加自己屏幕的相关信息
	1. 新增[[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c#struct panel_desc\|panel-simple.c#struct panel_desc]]类型变量
	2. 新增[[技术文档/Linux/Linux内核/源码结构/include/drm/drm_modes.h#struct drm_display_mode\|drm_modes.h#struct drm_display_mode]]类型变量
		1. 成员赋值参考





# 驱动源码修改

# 设备树修改

## 创建我的设备节点
```devicetree
panel_rgb: panel-rgb {

        compatible = "alientek,lcd-rgb";

        backlight = <&panel_backlight>;

        status = "okay";

  

        port {

            dsi_panel_in: endpoint {

                remote-endpoint = <&ltdc_ep1_out>;

            };

        };

    };
```

## LTDC节点修改
```devicetree

```

## 确定显示屏使用的引脚
在`pinctrl`节点中查找下述内容:
```devicetree
ltdc_pins_b: ltdc-b-0 {

        pins {

            pinmux = <STM32_PINMUX('I', 14, AF14)>, /* LCD_CLK */

                 <STM32_PINMUX('I', 12, AF14)>, /* LCD_HSYNC */

                 <STM32_PINMUX('I', 13, AF14)>, /* LCD_VSYNC */

                 <STM32_PINMUX('K',  7, AF14)>, /* LCD_DE */

                 <STM32_PINMUX('I', 15, AF14)>, /* LCD_R0 */

                 <STM32_PINMUX('J',  0, AF14)>, /* LCD_R1 */

                 <STM32_PINMUX('J',  1, AF14)>, /* LCD_R2 */

                 <STM32_PINMUX('J',  2, AF14)>, /* LCD_R3 */

                 <STM32_PINMUX('J',  3, AF14)>, /* LCD_R4 */

                 <STM32_PINMUX('J',  4, AF14)>, /* LCD_R5 */

                 <STM32_PINMUX('J',  5, AF14)>, /* LCD_R6 */

                 <STM32_PINMUX('J',  6, AF14)>, /* LCD_R7 */

                 <STM32_PINMUX('J',  7, AF14)>, /* LCD_G0 */

                 <STM32_PINMUX('J',  8, AF14)>, /* LCD_G1 */

                 <STM32_PINMUX('J',  9, AF14)>, /* LCD_G2 */

                 <STM32_PINMUX('J', 10, AF14)>, /* LCD_G3 */

                 <STM32_PINMUX('J', 11, AF14)>, /* LCD_G4 */

                 <STM32_PINMUX('K',  0, AF14)>, /* LCD_G5 */

                 <STM32_PINMUX('K',  1, AF14)>, /* LCD_G6 */

                 <STM32_PINMUX('K',  2, AF14)>, /* LCD_G7 */

                 <STM32_PINMUX('J', 12, AF14)>, /* LCD_B0 */

                 <STM32_PINMUX('J', 13, AF14)>, /* LCD_B1 */

                 <STM32_PINMUX('J', 14, AF14)>, /* LCD_B2 */

                 <STM32_PINMUX('J', 15, AF14)>, /* LCD_B3 */

                 <STM32_PINMUX('K',  3, AF14)>, /* LCD_B4 */

                 <STM32_PINMUX('K',  4, AF14)>, /* LCD_B5 */

                 <STM32_PINMUX('K',  5, AF14)>, /* LCD_B6 */

                 <STM32_PINMUX('K',  6, AF14)>; /* LCD_B7 */

            bias-disable;

            drive-push-pull;

            slew-rate = <105>;

        };

    };
    
    
ltdc_pins_sleep_b: ltdc-b-1 {

        pins {

            pinmux = <STM32_PINMUX('I', 14, ANALOG)>, /* LCD_CLK */

                 <STM32_PINMUX('I', 12, ANALOG)>, /* LCD_HSYNC */

                 <STM32_PINMUX('I', 13, ANALOG)>, /* LCD_VSYNC */

                 <STM32_PINMUX('K',  7, ANALOG)>, /* LCD_DE */

                 <STM32_PINMUX('I', 15, ANALOG)>, /* LCD_R0 */

                 <STM32_PINMUX('J',  0, ANALOG)>, /* LCD_R1 */

                 <STM32_PINMUX('J',  1, ANALOG)>, /* LCD_R2 */

                 <STM32_PINMUX('J',  2, ANALOG)>, /* LCD_R3 */

                 <STM32_PINMUX('J',  3, ANALOG)>, /* LCD_R4 */

                 <STM32_PINMUX('J',  4, ANALOG)>, /* LCD_R5 */

                 <STM32_PINMUX('J',  5, ANALOG)>, /* LCD_R6 */

                 <STM32_PINMUX('J',  6, ANALOG)>, /* LCD_R7 */

                 <STM32_PINMUX('J',  7, ANALOG)>, /* LCD_G0 */

                 <STM32_PINMUX('J',  8, ANALOG)>, /* LCD_G1 */

                 <STM32_PINMUX('J',  9, ANALOG)>, /* LCD_G2 */

                 <STM32_PINMUX('J', 10, ANALOG)>, /* LCD_G3 */

                 <STM32_PINMUX('J', 11, ANALOG)>, /* LCD_G4 */

                 <STM32_PINMUX('K',  0, ANALOG)>, /* LCD_G5 */

                 <STM32_PINMUX('K',  1, ANALOG)>, /* LCD_G6 */

                 <STM32_PINMUX('K',  2, ANALOG)>, /* LCD_G7 */

                 <STM32_PINMUX('J', 12, ANALOG)>, /* LCD_B0 */

                 <STM32_PINMUX('J', 13, ANALOG)>, /* LCD_B1 */

                 <STM32_PINMUX('J', 14, ANALOG)>, /* LCD_B2 */

                 <STM32_PINMUX('J', 15, ANALOG)>, /* LCD_B3 */

                 <STM32_PINMUX('K',  3, ANALOG)>, /* LCD_B4 */

                 <STM32_PINMUX('K',  4, ANALOG)>, /* LCD_B5 */

                 <STM32_PINMUX('K',  5, ANALOG)>, /* LCD_B6 */

                 <STM32_PINMUX('K',  6, ANALOG)>; /* LCD_B7 */

        };

    };
```

 