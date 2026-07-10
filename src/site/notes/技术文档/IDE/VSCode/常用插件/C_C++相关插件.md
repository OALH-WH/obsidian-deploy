---
{"dg-publish":true,"permalink":"/技术文档/IDE/VSCode/常用插件/C_C++相关插件/","dg-note-properties":{}}
---

# 插件
## C/C++
### 配置
#### c_cpp_properties.json
- `"includePath"`: 头文件查找路径
- `"browse.path"`: 源文件查找路径
#### settings.json
- `"C_Cpp.intelliSenseEngine"`: 指定插件智能感知引擎工作模式
	- `"Tag Parser"`: 模糊搜索模式
	- `"Default"`: 精确搜索模式
- `"C_Cpp.intelliSenseCachePath"`: 指定**预编译头文件 (PCH) 缓存**的位置
	- `eg. "C_Cpp.intelliSenseCachePath": "${workspaceFolder}/.vscode/intelliSenseCache"`: `intelliSenseCache`是一个目录
- `"C_Cpp.intelliSenseCacheSize"`: 单位`MB`
- `"C_Cpp.default.browse.databaseFilename"`: 指定**符号索引数据库**的位置
	- `eg. "C_Cpp.default.browse.databaseFilename": "${workspaceFolder}/.vscode/vc.db"`
	- 这个缓存文件基于智能感知引擎的`Default`模式
##### 注意
- **`intelliSenseCachePath` 是给你的“实时编辑器”加速的**：它影响的是你在敲代码时的体验，让智能提示更流畅。如果你的C盘空间紧张，或者想统一管理这些临时缓存，就应该修改这个路径
- **`databaseFilename` 是给你的“代码导航器”建档案的**：它直接影响你点击“转到定义”时的速度和准确性。结合你之前想用 Tag Parser 并获得类似 Source Insight 体验的需求，**强烈建议你将这个数据库文件设置到项目本地**
### 实例
#### 在开发大项目时, 响应缓慢(多个影响因素)
##### 场景
###### 生成了缓存, 但是缓存爆了
- 解决方法
	- 在`settings`中, 把`C_Cpp.intelliSenceCacheSize`设置为0
###### 引擎分析使用默认, 分析会非常慢
- 解决方法
	- 在`settings`中, 把`C_Cpp.intelliSenceEngine`设为`Tag Parser`

## C/C++ Extension Pack
## C/C++ Themes