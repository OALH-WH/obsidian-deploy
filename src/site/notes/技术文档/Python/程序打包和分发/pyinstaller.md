---
{"dg-publish":true,"permalink":"/技术文档/Python/程序打包和分发/pyinstaller/","dg-note-properties":{}}
---

# 依赖
- `pip install pyinstaller`
# 常见参数
- `--console`: 使用控制台子系统, **默认**
# 配置
- `<config file name>.spec`: 用于复杂项目的打包配置, 实际是个python脚本
### 依赖
- `from PyInstaller.utils.hooks import *
- `from PyInstaller.compat import is_win`
### 常见配置
#### `Analysis`配置: 主要配置
- `pathex`: 搜索模块的目录
#### `EXE`配置: 用于输出win系统可执行程序
#### `PYZ`配置

---
# 实例
## 生成spec基本框架
- `pyinstaller --onefile main.py`: 会在执行命令的目录下生成一个包含基本配置框架的spec文件
## 通过spec配置打包项目
- `pyinstaller <your spec file path>`
