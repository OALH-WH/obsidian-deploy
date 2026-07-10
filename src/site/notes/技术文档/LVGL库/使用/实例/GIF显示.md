---
{"dg-publish":true,"permalink":"/技术文档/LVGL库/使用/实例/GIF显示/","dg-note-properties":{}}
---

# GIF转C数组显示
## 依赖
- `lv_conf.h`中`LV_USE_GIF`置为`1`
- 用官方生成方法, 最后生成的的`.c`文件加入工程
- 在用到的源文件中用`LV_IMAGE_DECLARE(your_c_array_var_name)`声明你的`c`数组
- 

