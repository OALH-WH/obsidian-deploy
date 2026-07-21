---
{"dg-publish":true,"permalink":"/技术文档/构建工具/CMake/CMake语法/","dg-note-properties":{}}
---

# 语法格式
-  空格和换行作用相同，用于分隔参数
- 引用变量的方法
	- ${...}
# 基本框架
```cmake
project
```
# 常见内置变量
| 变量名                                 | 主要作用                                                           | 注意事项与说明                                                                                                                                                                                       |
| ----------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`CMAKE_ROOT`**                    | CMake 自身的安装目录。                                                 | 通常由 CMake 自动设置，用于查找其模块和配置文件，一般无需手动修改。                                                                                                                                                         |
| **`CMAKE_CXX_STANDARD`**            | **指定 C++ 语言标准版本**。例如 `11`, `14`, `17`, `20`。                   | 1. **与编译器参数的区别**：这是 CMake 提供的**跨编译器**统一设置方式，它会自动转换为对应编译器（如 `g++` 的 `-std=c++11`、`MSVC` 的 `/std:c++11`）的正确参数。  <br>2. **C/C++ 混编场景**：在需要链接 C 库时尤其方便，因为 `gcc` 命令不接受 `-std=c++11`，但 CMake 能正确处理。 |
| **`EXECUTABLE_OUTPUT_PATH`**        | 指定所有**可执行文件**（`add_executable` 的目标）的**输出目录**。                  | 设置此变量后，生成的可执行文件将被统一放置到指定路径，便于管理。                                                                                                                                                              |
| **`LIBRARY_OUTPUT_PATH`**           | 指定所有**库文件**（`add_library` 的目标，如 `.so`, `.a`, `.dll`）的**输出目录**。 | 同上，用于集中管理生成的库文件。                                                                                                                                                                              |
| **`CMAKE_EXPORT_COMPILE_COMMANDS`** | 生成 `compile_commands.json` 文件。                                 | 该文件被许多**代码分析工具**（如 `clangd`, `ccls`）用于提供精确的**代码补全、跳转和错误检查**。通常通过 `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` 启用。                                                                                     |
| **`CMAKE_MAKE_PROGRAM`**            | **手动指定生成工具（构建系统）的路径**。                                         | 当 CMake 无法自动找到 `make`, `ninja` 等工具，或你想使用特定版本时使用。例如：`-DCMAKE_MAKE_PROGRAM=/usr/local/bin/ninja`。                                                                                               |
| **`CMAKE_CURRENT_SOURCE_DIR`**      | 表示**当前正在处理**的 `CMakeLists.txt` 文件所在的**目录**。                    | 这是一个“动态”变量，随着 CMake 处理子目录而变化。                                                                                                                                                                 |
| **`PROJECT_SOURCE_DIR`**            | 表示**最近一次调用 `project()` 命令**的 `CMakeLists.txt` 所在的**目录**。       | 如果项目在子目录中调用 `project()`，该变量将指向该子目录，而非最顶层目录。                                                                                                                                                   |
| **`CMAKE_SOURCE_DIR`**              | 表示**最顶层** `CMakeLists.txt` 所在的**目录**。                          | 这是整个项目的**源码根目录**，其值在配置过程中**固定不变**。                                                                                                                                                            |
| **`PROJECT_BINARY_DIR`**            | 表示**当前项目**（最近一次 `project()`）的**构建输出目录**。                       | 通常对应 `project()` 所在目录下的 `CMakeCache.txt` 所在位置。随 `project()` 调用位置和构建目录变化。                                                                                                                      |
| **`CMAKE_BINARY_DIR`**              | 表示**项目最顶层**的**构建输出目录**（即执行 `cmake` 命令的目录）。                     | 其值在配置时确定，**固定不变**。例如执行 `cmake -S . -B build` 时，该变量即为 `./build`。                                                                                                                               |
| `CMAKE_BUILD_TYPE`                  | 表示构建类型 (即构建目标的可调式级别, 常见的有`Debug Release`)                      | `Debug`: 启用调试信息, 通常不进行优化, 便于调试, 即保证把编译器选项`-g`加上<br>`Release`: 会优化代码, 通常不包含调试信息                                                                                                                |
| `CMAKE_VERBOSE_MAKEFILE`            | 开启用于在`makefile`构建过程中, 打印实际执行的命令                                | 其值为ON of OFF                                                                                                                                                                                  |
| `CMAKE_LIBRARY_PATH`                | 要链接的库的搜索路径                                                     |                                                                                                                                                                                               |
| ``CMAKE_FIND_ROOT_PATH``            | 不推荐使用, 建议使用`CMAKE_SYSROOT`                                     |                                                                                                                                                                                               |
| ``CMAKE_SYSROOT``                   | 手动指定编译器所使用的`sysroot`路径, 最终会通过`--sysroot`参数传递给编译器               |                                                                                                                                                                                               |

## 关于四个目录变量的核心区别

- 您提到的 `PROJECT_SOURCE_DIR`、`CMAKE_SOURCE_DIR`、`PROJECT_BINARY_DIR`、`CMAKE_BINARY_DIR` 这四个变量容易混淆，它们的核心区别在于“作用域”和“是否可变”：
	- **`PROJECT_` 开头**的变量，其值与**最近一次调用 `project()` 命令的位置**相关，是**项目作用域**的。
	- **`CMAKE_` 开头**的变量，其值指向**整个 CMake 构建的最顶层**，是**全局作用域**的，在配置期间**固定不变**。
	- **`_SOURCE_`** 指向**源代码**目录。
	- **`_BINARY_`** 指向**构建输出**目录。
- **简单来说，`CMAKE_` 是“全局的、固定的”，而 `PROJECT_` 是“局部的、可变的”。**
---
# 常见函数/方法
### 一、 项目配置与基本信息

#### 1. `project()` - 定义项目

- **作用**：定义项目名称，并声明项目支持编译的编程语言。
    
- **格式**：`project(<PROJECT-NAME> [LANGUAGES] [CXX] [C] ...)`
    
- **示例**：`project(MyDemo LANGUAGES CXX C)` 表示项目名为 `MyDemo`，支持编译 C++ 和 C 文件。
    

#### 2. `cmake_minimum_required()` - 设置最低版本

- **作用**：设置构建本项目所需的 CMake 最低版本。
    
- **格式**：`cmake_minimum_required(VERSION <min>[...<max>])`
    
- **示例**：`cmake_minimum_required(VERSION 3.25)`。
    

---

### 二、 变量、消息与函数

#### 1. `set()` - 设置变量

- **作用**：设置一个普通变量、缓存变量或环境变量的值。
    
- **格式**：`set(<variable> <value>... [CACHE <type> <docstring> [FORCE]])`
    
- **示例**：
    
    cmake
    
    set(SRC_LIST main.cpp) # 设置普通变量
    set(CMAKE_EXPORT_COMPILE_COMMANDS ON) # 生成编译数据库，用于代码补全等工具
    # 设置默认生成器和 make 程序路径（写入缓存，强制生效）
    set(CMAKE_GENERATOR “Unix Makefiles” CACHE STRING “Default generator” FORCE)
    set(CMAKE_MAKE_PROGRAM “D:/path/to/make.exe” CACHE STRING “Default make program” FORCE)
    

#### 2. `message()` - 输出消息

- **作用**：在配置或构建过程中打印消息，用于调试或提示。
    
- **格式**：`message([<mode>] “message text” …)`
    
- **常用模式**：
    
    - `STATUS`：前缀为 `--` 的信息（常用）。
        
    - `WARNING`：CMake 警告，会继续执行。
        
    - `AUTHOR_WARNING`：开发者警告。
        
    - `SEND_ERROR`：CMake 错误，继续执行但会停止生成。
        
    - `FATAL_ERROR`：CMake 错误，立即停止。
        
- **示例**：`message(STATUS “Build type: ${CMAKE_BUILD_TYPE}”)`
    

#### 3. `function()` / `endfunction()` - 定义函数

- **作用**：定义一个可以重用的 CMake 函数。
    
- **格式**：
- ```cmake
function(func_name arg1 arg2…)
	# 函数体
	# 使用 ${arg1}, ${arg2} 访问参数
endfunction()
    ```

---

### 三、 构建目标 (Target) 操作

#### 1. `add_executable()` - 添加可执行目标

- **作用**：使用指定的源文件列表生成一个可执行文件目标。
    
- **格式**：`add_executable(<name> [WIN32] [MACOSX_BUNDLE] [source1] [source2] …)`
    
- **示例**：`add_executable(demo ./src/main.cc ./src/test.c)`
    
- **常见问题**：`set()` 命令本身**不会解析通配符**（如 `*.cpp`），直接将其值传给 `add_executable` 会导致找不到文件。应使用 `file(GLOB ...)` 或显式列出所有文件。
    

#### 2. `add_library()` - 添加库目标

- **作用**：将指定的源文件编译成库文件（静态库、动态库等）。
    
- **格式**：`add_library(<name> [STATIC | SHARED | MODULE] [source1] [source2] …)`
    
- **示例**：`add_library(mylib SHARED ./src/test.c)` 生成动态库 `libmylib.so`（Linux）或 `mylib.dll`（Windows）。
    
- **注意**：目标名（`mylib`）本身**不带 `lib` 前缀**。
    

#### 3. `target_link_libraries()` - 链接库

- **作用**：为指定的目标（可执行文件或库）链接其他库。
    
- **格式**：`target_link_libraries(<target> [PRIVATE | PUBLIC | INTERFACE] <item>… )`
    
- **示例**：`target_link_libraries(demo PRIVATE mylib)` 将库 `mylib` 链接到目标 `demo`。
    
- **链接可见性**：
    
    - `PRIVATE`：仅当前目标使用。
        
    - `PUBLIC`：当前目标使用，并传递给链接它的其他目标。
        
    - `INTERFACE`：当前目标不使用，但传递给链接它的其他目标。
        

#### 4. `target_include_directories()` - 添加头文件目录

- **作用**：为指定的目标添加头文件搜索路径。
- **格式**：`target_include_directories(<target> [SYSTEM] [BEFORE] <INTERFACE|PUBLIC|PRIVATE> [items…])`
- **示例**`target_include_directories(demo PUBLIC ${PROJECT_SOURCE_DIR}/inc)`。`PUBLIC` 意味着使用 `demo` 的目标也会自动包含此目录。
#### 5. `include_directories()` - (全局)添加头文件目录

- **作用**：为**当前目录及以下**的所有目标添加头文件搜索路径（较旧的方法，现代 CMake 推荐使用 `target_include_directories`)。
    
- **示例**：`include_directories(./inc)`
    

---

### 四、 文件与目录操作

#### `file(GLOB …)` - 生成文件列表

- **作用**：使用通配符匹配，生成一个文件列表并存入变量。
    
- **格式**：`file(GLOB <variable> [LIST_DIRECTORIES true|false] [<globbing-expr>…])`
    
- **示例**：`file(GLOB SOURCES “./src/*.cc” “./src/*.c”)` 将所有 `.cc` 和 `.c` 文件列表存入 `SOURCES` 变量。
    

#### `install()` - 安装目标/文件

- **作用**：定义安装规则，将目标、文件或目录安装到指定位置（在 `make install` 时执行）。
    
- **格式**：`install(TARGETS <target>… DESTINATION <dir>)`，`install(FILES <file>… DESTINATION <dir>)`
    
- **示例**：
    
    cmake
    
    install(TARGETS demo DESTINATION bin) # 安装可执行文件到 ${CMAKE_INSTALL_PREFIX}/bin
    install(FILES config.ini DESTINATION etc) # 安装配置文件
    
- **注意**：安装库目标时，目标名同样不带 `lib` 前缀。
    
#### find_library()
- 作用: 用于在指定目录下搜索库文件的路径
- 格式: `find_library()`
---

### 五、 自定义构建步骤与命令

#### 1. `add_custom_target()` - 添加自定义目标

- **作用**：添加一个**没有输出**的自定义目标，它总是会被构建（除非指定了 `ALL` 参数且没有默认构建）。
    
- **格式**：
    ```cmake
    add_custom_target(<Name> [ALL]
                      [COMMAND command1 [ARGS ...]]
                      [COMMAND command2 ...]
                      ...)
    ```
- **参数**：
    
    - `ALL`：指定后，该目标会被包含在默认构建目标中（即运行 `make` 时会执行它）。
        
- **示例**：`add_custom_target(run_tests ALL COMMAND ./my_test_tool)`。
    

#### 2. `add_custom_command()` - 添加自定义命令
- **参数**
	- `TARGET <actual_target>`: 指定构建目标, `eg. TARGET main`
	- `POST_BUILD | ...`
		- `POST_BUILD`: 目标构建后执行
	- `COMMAND <actual_command>`: 指定自定义命令
- **作用**：为生成**特定输出文件**添加自定义构建规则。通常与 `add_custom_target` 或 `add_dependencies` 配合使用。
- **注意**：它定义了**如何产生文件**，而不是定义一个“总是运行”的目标。
#### 3. `execute_process()` - 执行进程
- **作用**：在 **CMake 配置阶段**（运行 `cmake` 时）执行一个或多个外部命令或进程。
- **格式**：
```cmake
execute_process(COMMAND <cmd1> [args...]
                    [WORKING_DIRECTORY <directory>]
                    [COMMAND_ECHO <STDOUT|...>]
                    [OUTPUT_VARIABLE <variable>]
                    [RESULT_VARIABLE <variable>]
                    ...)
```
- **示例**：`execute_process(COMMAND git --version OUTPUT_VARIABLE GIT_VER)`。
---

### 六、 查找与使用外部包 (Package)

#### 1. `find_package()` - 查找包

- **作用**：查找并加载外部项目的设置。`find_package(PkgConfig REQUIRED)` 是使用 `pkg-config` 工具的前置条件。
- **工作模式**：
    - **`MODULE` 模式**：优先查找名为 `Find<PackageName>.cmake` 的模块文件。
        - 搜索路径（优先级降序）：1. `CMAKE_MODULE_PATH` 变量；2. CMake 安装目录下的 `Modules` 目录。
    - **`CONFIG` 模式**：查找名为 `<PackageName>Config.cmake` 的配置文件。
- **参数**：
    - `REQUIRED`：必须找到该包，否则停止。
    - `MODULE` / `CONFIG`：强制指定查找模式。
- **示例**
	- `find_package(OpenCV REQUIRED)`
    

#### 2. `pkg_check_modules()` - 通过 pkg-config 查找

- **作用**：通过系统的 `pkg-config` 工具（查找 `.pc` 文件）来定位外部库，并将其信息封装为 CMake 变量或 **IMPORTED target**。
    
- **格式**：`pkg_check_modules(<PREFIX> [REQUIRED] [IMPORTED_TARGET] <moduleSpec>…)`
    
- **影响**：成功后会填充一系列变量（以 `<PREFIX>` 开头）：
- |变量|含义|
    |---|---|
    |`<PREFIX>_FOUND`|1 表示找到|
    |`<PREFIX>_INCLUDE_DIRS`|头文件搜索路径列表|
    |`<PREFIX>_LIBRARIES`|需要链接的库名列表|
    |`<PREFIX>_LIBRARY_DIRS`|库文件搜索路径|
    |`<PREFIX>_CFLAGS_OTHER`|额外编译标志|
    |`<PREFIX>_LDFLAGS_OTHER`|额外链接标志|
- **示例**：
```cmake
    find_package(PkgConfig REQUIRED)
    pkg_check_modules(FMT REQUIRED IMPORTED_TARGET fmt) # 查找 fmt 库
    # 这会生成一个名为 PkgConfig::FMT 的导入目标，可直接链接
    target_link_libraries(demo PRIVATE PkgConfig::FMT)
```


### 逻辑函数
#### if()

##### 基本格式
`if(<expression>)`

**参数**
- `expression`:
	- `DEFINED | NOT DEFINED <VAR>`: 判断变量是否存在
		- `eg. if(DEFINED MY_VAR)`
#### endif()
配合[[技术文档/构建工具/CMake/CMake语法#if()\|#if()]]使用