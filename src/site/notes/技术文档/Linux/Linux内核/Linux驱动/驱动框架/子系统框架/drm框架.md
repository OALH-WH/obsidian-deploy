---
{"dg-publish":true,"permalink":"/技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/drm框架/","dg-note-properties":{}}
---

# 背景
`Direct Render Manager`

## 关系
### 驱动和子系统之间的关系
[[技术文档/Linux/Linux内核/Linux驱动/驱动框架/子系统框架/resources/Drawing 2026-06-12 13.12.08.excalidraw\|Drawing 2026-06-12 13.12.08.excalidraw]]
### 对象之间的关系
![Pasted image 20260611193136.png](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Linux/Linux%E5%86%85%E6%A0%B8/Linux%E9%A9%B1%E5%8A%A8/%E9%A9%B1%E5%8A%A8%E6%A1%86%E6%9E%B6/%E5%AD%90%E7%B3%BB%E7%BB%9F%E6%A1%86%E6%9E%B6/resources/Pasted%20image%2020260611193136.png)
在DRM的**内核模式设置（KMS）** 中，有5个核心对象，它们共同构成了一条完整的显示数据流水线[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)。

1. **Framebuffer (帧缓冲)**：**内存中的显示数据**。它是一个内存缓冲区，存储了要显示的像素数据[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)。它不直接与硬件交互，而是通过**Plane**被硬件消费[](https://www.eet-china.com/mp/a186423.html)。
    
2. **Plane (平面)**：**图像数据的来源与合成**。它从Framebuffer中读取数据，并可进行缩放、裁剪等操作[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)。一个**CRTC**可以由一个或多个Plane提供数据，经过合成后输出[](https://docs.kernel.org/6.2/gpu/drm-kms.html#c.drm_crtc_set_max_vblank_count)。它是连接Framebuffer和CRTC的纽带[](https://www.eet-china.com/mp/a186423.html)。
    
3. **CRTC (CRT Controller)**：**显示管线的核心控制器**。它从Plane接收合成后的图像数据，并按照特定的**显示模式（如分辨率、刷新率）** 生成扫描时序[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)[](https://docs.kernel.org/6.2/gpu/drm-kms.html#c.drm_crtc_set_max_vblank_count)。CRTC的数量决定了系统能同时支持多少个独立的显示输出[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)。
    
4. **Encoder (编码器)**：**数据格式转换器**。它将CRTC输出的像素数据，转换为适合特定物理接口（如HDMI、DP、LVDS）的电气信号格式[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)[](https://docs.kernel.org/6.2/gpu/drm-kms.html#c.drm_crtc_set_max_vblank_count)。它是连接CRTC和Connector的纽带[](https://www.eet-china.com/mp/a186423.html)。
    
5. **Connector (连接器)**：**物理连接的终点**。它代表设备上的物理显示输出端口（如HDMI接口、DP接口、eDP接口），并负责与实际的显示设备（显示器、面板）进行通信和协商[](https://manpages.debian.org/experimental/libdrm-dev/drm-kms.7.en.html)[](https://docs.kernel.org/6.2/gpu/drm-kms.html#c.drm_crtc_set_max_vblank_count)。

## 驱动加载与显示初始化流程图（时序）
```text

  内核启动
     |
     v
+-------------+
| 设备树解析   |
+-------------+
     |
     | 匹配 compatible 属性
     +--------------------------+--------------------------+
     |                          |                          |
     v                          v                          v
+------------+           +-------------+           +-------------+
| Panel 驱动  |           | LTDC 驱动   |           | 桥片驱动(若有)|
| probe()    |           | probe()     |           | probe()     |
+------------+           +-------------+           +-------------+
     |                          |                          |
     | drm_panel_add()          |                          |
     | (注册panel到全局列表)     |                          |
     |                          |                          |
     |                          | drm_of_find_panel_or_bridge()
     |<-------------------------| (通过设备树端口查找panel)  |
     |                          |                          |
     |                          | drm_dev_alloc/register   |
     |                          |   -> 创建 CRTC, Encoder  |
     |                          |   -> 绑定 Connector 到 Panel
     |                          |                          |
     |                          |                         (桥片可能注册Encoder)
     |                          |                          |
     +----------------------------+--------------------------+
                               |
                               v
                    +---------------------+
                    | DRM 设备注册完成      |
                    | 创建 /dev/dri/card0  |
                    +---------------------+
                               |
                               v (用户空间如 weston 发起)
                    +---------------------+
                    | drm_mode_set_crtc    |
                    | (设置显示模式)        |
                    +---------------------+
                               |
          +--------------------+--------------------+
          |                    |                    |
          v                    v                    v
   +-------------+     +-------------+       +-------------+
   | LTDC 驱动    |     | Panel 驱动   |       | 背光/电源   |
   | mode_set     |     | prepare()   |       | 驱动        |
   | (配置时序)   |     | (上电/初始化)|       | 使能背光    |
   +-------------+     +-------------+       +-------------+
          |                    |                    |
          +--------------------+--------------------+
                               |
                               v
                    +---------------------+
                    | 正常显示画面          |
                    | LTDC 从内存扫描输出   |
                    +---------------------+
```
**流程关键点**
1. **Probe 顺序**：Panel 驱动通常先加载并注册自身（`drm_panel_add`）。LTDC 驱动随后 probe，通过设备树查找已注册的 Panel，并建立连接。
2. **显示通路建立**：DRM 框架将 LTDC 的 CRTC 和 Panel 的 Connector 关联起来。
3. **运行时**：用户空间通过 DRM KMS 接口设置显示模式，触发 LTDC 配置硬件时序，随后调用 Panel 的 `prepare` / `enable` 使屏幕正常工作。
# 使用参考
- [[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/panel-simple.c\|panel-simple.c]]

# 驱动依赖
- [[技术文档/Linux/Linux内核/源码结构/drivers/gpu/drm/stm/drv.c\|drv.c]]
## ltdc驱动

# 设备树依赖
## ltdc节点
### port节点
#### endpoint节点