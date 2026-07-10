---
{"dg-publish":true,"permalink":"/技术文档/Linux/linux常用操作/文本处理相关/awk命令/","dg-note-properties":{}}
---

1. 内置变量

1. NR：表示行号

1. NF: 表示当前行的字段数

1. 语法

1. 条件，动作模式

1. 描述：M {N}表示模式M匹配到的行，执行N动作

1. 范围模式

1. 描述：M,N用于选择从模式M匹配的行开始到模式N匹配的行结束

1. 示例：/pattern/，/pattern/

1. 正则匹配（通过/pattern/来匹配）

1. 常用函数

1. mawk(posix标准): match

1. 作用：把正则匹配的内容存到变量，不支持正则扩展

1. 参数

1. arg1：表示获取正则匹配到的内容,可以认为是一个变量

1. arg2：/patern/

1. 返回值

1. 匹配到了为true，否则为false

1. 隐藏返回值

1. RSTART：字符串起始索引

1. RLENGTH：字符串长度

1. gawk(gnu, 兼容mawk用法): match

1. 作用：把捕获的内容存到变量中

1. 参数

1. arg1:表示匹配的内容

1. arg2:/pattern/

1. arg3:数组变量，索引0对应匹配到的全部内容，索引1对应第一个捕获组内容

1. 返回值

1. 匹配到了为true，否则为false

1. 隐藏返回值

1. RSTART：匹配的字符串起始索引

1. RLENGTH：匹配的字符串长度

1. length

1. 作用

1. 获取字符串的长度

1. substr

1. 作用

1. 返回指定的子串

1. 参数

1. arg1：存储字符串的变量

1. arg2：起始索引，最低0

1. arg3：长度

1. 实例

1. s = substr(...); print s

1. print

1. eg.{print $1 ":" $2} //输出$1和$2匹配到的内容，并通过":"拼接

1. next

1. 不执行后面的语句,直接解析下一行

1. 使用示例

1. 匹配到一行之后打印之后的所有内容

1. awk '/pattern/,0' file.txt

1. awk 'found {print} /pattern/ {found=1}' file.txt

1. 匹配非指定字符的所有内容

1. awk '!/pattern/' file.txt

1. 实例

1. 匹配在某些子串基础上，path相同的行，并输出

```cpp

gawk '
 /component.*isSyncDone = true/ {
    if (match($0, /path = (\/openconfig-platform:components\/component.*), isTerminated/, arr)) {
        key=arr[1]
        paths[key] = 1
        print
    }
    
}
/payload is invalid, no push/ {
    if (match($0, /path=(.*) payload/, p)) {
        path = p[1]
        if (path in paths) {
            print 
        }
    }
}
 ' telemetry.log > test.log
```