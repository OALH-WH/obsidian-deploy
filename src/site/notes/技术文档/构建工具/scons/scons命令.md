---
{"dg-publish":true,"permalink":"/技术文档/构建工具/scons/scons命令/","dg-note-properties":{}}
---

# 参数
- `-j<num>`: 多核编译, 比如`-j8`表示`8`核编译
- `-c`: 清除项目过程文件
- `--pyconfig`: 打开`KConfig`的配置界面, 基于`python`实现的UI
	- 需要`ENV_ROOT`环境变量, 去指定`env`可执行文件的目录
	- 使改动生效可以通过命令`scons --pyconfig-silent`

---
- 实例

	- 生成compile_commands.json

		- 执行以下命令

			- env.Tool('compilation_db')

			- env.CompilationDatabase()

- 构建命令

	- scons

		- 参数

			- -c:清除构建过程中产生的中间文件和目标文件

- env字典的键

	- bindir：构建的可执行文件的路径

- sconscript：用来指定哪些文件会加入编译

	- 常用内置函数

		- Clean函数：指定删除的文件

		- NoClean函数：指定不能删除的文件

		- Environment：创建环境对象

			- env.Append（）：添加编译选项

		- Import()：引用传入的参数

		- Sconscript：调用Sconscript文件

			- 示例：

```cpp
#SConstruct
env = Environment()
SConscript('lib/SConscript', exports='env')

#SConscript
Import("env")

env.Program()
```

		- Default：用来指定构建时的默认目标，这些目标可以是Program，Library，Shared'L'i'b

		- Replace:自定义编译选项

			- 示例：

```
env.Replace(
    CCFLAGS=['-Wall', '-O2', '-g'],  # 通用编译选项
    CFLAGS=['-std=c99'],             # C语言特定选项
    LINKFLAGS=['-lm']                # 链接选项，例如链接数学库
)
```

		- Dir() :获取路径

			- 示例

				- Dir(".")：获取当前sconscript的路径

				- Dir("#")：获取项目Sconsturct的路径

		- Glob('*.c') :获取当前目录下的所有C文件

			- 返回值：字符串列表

		- GetDepend(macro) :在tools/目录下的脚本文件中定义，它会从rtconfig.h文件读取组件配置信息，其参数为rtconfig.h中的宏名。如果rtconfig.h打开了某个宏，则这个方法（函数）返回真，否则返回假。

		- Split() :将字符串str分割成一个list

		- DefineGroup(name, src, depend, **parameters) ：这是RT-Thread基于SCons扩展的一个方法（函数）。DefineGroup用于定义一个组件。组件可以是一个目录（下的文件或子目录），也是后续一些IDE工程文件中的一个Group或文件夹。

			- name来定义这个group的名字

			- src用于定义这个Group中包含的文件，一般指的是C/C++源文件。方便起见，也能够通过Glob函数采用通配符的方式列出SConscript文件所在目录中匹配的文件。

			- depend 用于定义这个Group编译时所依赖的选项（例如finsh组件依赖于RT_USING_FINSH宏定义）。编译选项一般指rtconfig.h中定义的RT_USING_xxx宏。当在rtconfig.h配置文件中定义了相应宏时，那么这个Group才会被加入到编译环境中进行编译。如果依赖的宏并没在rtconfig.h中被定义，那么这个Group将不会被加入编译。相类似的，在使用scons生成为IDE工程文件时，如果依赖的宏未被定义，相应的Group也不会在工程文件中出现。

			- parameters则可以输入一组字符串，后面还可以加入的参数包括：

				- CCFLAGS – C源文件编译参数；

				- CPPPATH – 头文件路径；

				- CPPDEFINES – 添加预定义宏；

				- LINKFLAGS – 链接时参数。

				- LIBRARY – 包含此参数，则会将组件生成的目标文件打包成库文件可见DefineGroup的功能十分强大，实际使用时不需要配置所有参数。

		- SConscript(dirs, variant_dir, duplicate) :

			- Cons内置函数。其参数包括三个：

				- dirs指明SConscript文件路径，

				- variant_dir指定生成的目标文件的存放路径，

				- duiplicate的作用是设定是否拷贝或链接源文件到variant_dir

- sconstrcut：用来编译指定的文件，一个项目中只能有一个

- Sconscript：用来寻找子目录下是否有其他Sconscript，一个项目中可以有多个

- SconStruct和SconScript联合使用

	- 由SconStruct中定义构建对象，然后通过Sconscript函数调用指定路径下的Sconscript文件