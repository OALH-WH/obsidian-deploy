---
{"dg-publish":true,"permalink":"/技术文档/Linux/脚本/shell脚本/","dg-note-properties":{}}
---

## 1. 命令块 `{}`

- `{}` 中的命令 **前后必须有空格**
    
- 语句结尾需要 `;` 或换行
    

`{ ls; pwd; }`

---

## 2. 分隔符规则

- **空格和换行符** 都可以作为命令或变量的分隔符
    
- Shell 以 **token** 为解析单位
    

---

## 3. 执行脚本的方式

### 3.1 创建子进程执行

`./path/script.sh`

- 创建 **子进程**
    
- 子进程中的变量 **不会影响当前 shell**
    

---

### 3.2 当前 shell 中执行

`. ./path/script.sh # 等价 source ./path/script.sh`

- **不创建子进程**
    
- 变量、函数、cd 等都会影响当前环境
    

---

## 4. 重定向操作

### 4.1 `<`（标准输入重定向）

- 将文件内容作为命令的标准输入
    

`cmd < file`

#### 实例
##### 多行注释
```shell
: << 'EOF'
...
EOF
```

---

### 4.2 `<<`（Here Document）

- 将 **多行内容** 作为命令的标准输入
    

`ls << EOF 第一行内容 第二行内容 EOF`

---

### 4.3 `<<<`（Here String，bash 扩展）

- 将 **字符串** 作为命令的标准输入
    
- 类似管道
    

`cat <<< "hello world"`

---

## 5. 字符串与算术

### 5.1 `$'...'`（支持转义字符，bash 扩展）

`echo $'line1\nline2'`

---

### 5.2 算术运算

`$((a + b))`

- 支持 `+ - * / % **`
- 支持变量自增自减
	- `((i++))`

---

### 5.3 `()` 提升优先级

`$(( (a + b) * c ))`

---

## 6. 常见内建命令

- `eval`
    
    - 对字符串 **进行两次解析**
        
    - 风险较高，慎用
        
- `let`
    
    - 整数运算（当前 shell 有效）
        
- `sync`
    
    - 将缓冲区数据写入磁盘
        
- `nohup`
    
    - 创建新会话运行程序
        
    - 默认输出到 `nohup.out`
        

`nohup cmd > out.log 2>&1 &`

---

## 7. 数组（bash / zsh）

### 7.1 定义数组

`arr=("1" "2" "3")`
#### 7.1.1 从命令行定义数组
- `mapfile -t arr < <(command)`
- `arr=($(command))`
---

### 7.2 数组追加

`arr+=("4")`

---

### 7.3 数组长度

`${#arr[@]}`

---

### 7.4 获取数组元素

`${arr[@]}`

---

## 8. 内置变量（特殊参数）

- 详情参考[[技术文档/Linux/Shell/内建变量_命令\|内建变量_命令]]

| 变量      | 含义                      |
| ------- | ----------------------- |
| `$EUID` | 当前进程的有效用户 ID            |
| `$0`    | 脚本名（包含路径）               |
| `$?`    | 上一个命令的退出状态              |
| `$#`    | 参数个数（不含 `$0`）           |
| `$@`    | 参数列表（推荐用 `"$@"`）        |
| `$*`    | 所有参数作为一个字符串             |
| `$-`    | shell 选项标志（含 `i` 表示交互式） |

---

## 9. 条件判断（test / `[ ]`）

### 9.1 文件测试

| 选项   | 含义                                                  |
| ---- | --------------------------------------------------- |
| `-f` | 常规文件                                                |
| `-d` | 目录                                                  |
| `-e` | 存在                                                  |
| `-b` | 块设备                                                 |
| `-t` | 判断文件描述符是否打开且与终端相关联<br>`eg. [ -t 1 ]`表示判断标准输出是否输出到终端 |

---

### 9.2 字符串测试

| 选项       | 含义    |
| -------- | ----- |
| `-z str` | 字符串为空 |

**示例**
- `[ str1 <= str2 ]   # 字符串比较`
- `eg. [ str1 = str2 ]`: `POSIX`兼容写法 

---

### 9.3 数值比较

| 运算符   | 含义   |
| ----- | ---- |
| `-eq` | 等于   |
| `-le` | 小于等于 |
| `-gt` | 大于   |

---

### 9.4 逻辑运算

| 运算符  | 含义    |
| ---- | ----- |
| `-a` | 与（&&） |
| `-o` | 或（    |

---

## 10. 函数定义

### 10.1 POSIX 写法（推荐）

`my_func() {     statements }`

---

### 10.2 bash/zsh 扩展写法

`function my_func() {     statements }`

---

## 11. select 语句（bash）

```shell
select i in ${arr[@]}; do
    case $i in
        "str1") break ;;
        "str2") break ;;
        *) break ;;
    esac
done
```
---

## 12. 循环结构

### 12.1 for 循环
`for i in 1 2 3; do     statements done`
`# bash 扩展 for i in {1..5}; do     statements done`
#### 12.1.1 遍历数组(bash或zsh)
- 不加引号处理逻辑, `eg. for i in ${arr[@]}; do     statements done`
	- 
- 加引号处理逻辑, `eg. for i in "${arr[@]}"; do     statements done`
	- 
---

### 12.2 while 循环

`while true; do     statements done`

`while [ condition ]; do     statements done`

---

## 13. if 判断

`if [ condition ]; then     statements elif [ condition ]; then     statements else     statements fi`

---

## 14. 实例：字符串转字节数据

`printf "%b" "\x12\x34" > file`

`printf "\x12\x34" > file`

---

## 15. 常用命令速查

### 15.1 seq

`seq 1 2 # 输出： # 1 # 2`

---

### 15.2 readarray / mapfile（bash）

`readarray -t arr < <(cmd)`

- `-t`：去除换行符
    
- `<()`：进程替换（bash）
    

---

### 15.3 printf

`printf "hello world %d\n" 1`

---

### 15.4 script

`script -q -c "cmd" output.log scriptreplay output.log`

---

### 15.5 yes

`yes yes no`

---

### 15.6 其他

`echo "msg" exit 0 sleep 1 usleep 1 shift 1 unset var`

---

## 16. 数学运算工具

### 16.1 expr（十进制）

`expr $i + $j`

> 使用 `()` 需要转义

---

### 16.2 let / (( ))

`let "i=i+1" ((i++))`

---

## 17. 运算符总结

|运算符|含义|
|---|---|
|`+`|加|
|`-`|减|
|`*`|乘|
|`/`|除|
|`%`|取余|
|`++`|自增|
|`--`|自减|
|`**`|幂运算（bash）|
# 18. 变量引用
## 18.1 bash/zsh扩展
|语法|含义|是否POSIX|
|---|---|---|
|`${var:-default}`|var为空或未设置时用default|**否**，bash/ksh扩展|
|`${var-default}`|仅var未设置时用default|**否**，bash/ksh扩展|
|`${var:=default}`|var为空时设default并赋值|**否**，bash/ksh扩展|
|`${var:?error}`|var为空时报错退出|**否**，bash/ksh扩展|
