---
{"dg-publish":true,"permalink":"/技术文档/构建工具/scons/子级Sconscript/","dg-note-properties":{}}
---

1. 示例

```cpp
from building import *

cwd     = GetCurrentDir()
src     = Split('''
shell.c
msh.c
msh_parse.c
''')

if GetDepend('MSH_USING_BUILT_IN_COMMANDS'):
    src += ['cmd.c']

if GetDepend('DFS_USING_POSIX'):
    src += ['msh_file.c']

CPPPATH = [cwd]

group = DefineGroup('Finsh', src, depend = ['RT_USING_FINSH'], CPPPATH = CPPPATH)

Return('group')

```