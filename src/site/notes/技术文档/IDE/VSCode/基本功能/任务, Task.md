---
{"dg-publish":true,"permalink":"/技术文档/IDE/VSCode/基本功能/任务, Task/","dg-note-properties":{}}
---

# 配置
## 属性
- `label`
- `command`
- `type`: 指定任务类型, 比如一个`shell`任务
- `problemMatcher`: 问题匹配器, 用来处理任务输出, 问题匹配器会扫描任务输出文本中已知的警告或错误字符串，并将其内联报告在编辑器中以及“问题”面板中。VS Code 内置了几个问题匹配器
- `options`: 其他选项
	- `cwd`: 执行任务的工作目录
	- `shell`: 配置可能使用的`shell`
		- `executable`: 指定可执行程序, 比如`git bash`, `powershell`, `cmd`等
		- `args`: 指定`shell`参数
- `group`: 分组配置, 目前就支持`build`和`test`
	- `kind`: 指定分组, `eg. build or test`
# 使用
## 快捷键
- 触发构建任务: `ctrl + shift + b`

---
1. 创建task template

2. 步骤

3. 工具栏->terminal->congfigure Tasks

4. 选择一个模板

5. 执行task

6. 步骤

7. 工具栏->terminal->run task //显示所有可执行的任务

8. 选择你要执行的任务，任务名为定义的label

9. task语法

10. tasks列表

11. 作用

12. 存储了所有的task

13. task对象

14. 任务输出控制

15. 终端=看原始日志，problemMatcher=把错误变“可点击”，自定义 presentation=让输出更干净。把上面三段 JSON 按需组合即可。

16. label：标签

17. type：

18. command：要执行的命令

19. detail：详细描述

20. problemMatcher