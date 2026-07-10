---
{"dg-publish":true,"permalink":"/技术文档/Python/第三方包/python 第三方库/","dg-note-properties":{}}
---

1. random

1. 

1. struct

1. unpack方法：按照规则，解包字节流，输入为bytes， 常用于协议解析

1. fomat

1. 字节序

1. >：大端

1. <：小端

1. !：网络字节序

1. =：本机字节序

1. @：本机字节序和大小

1. 格式字符串

1. H：无符号短整型，2bytes

1. i: 整型，4bytes

1. I：四字节无符号整型

1. flask：轻量级的web应用框架

1. 安装：pip install Flask

1. 给前端发送一个页面显示

1. return render_template('index.html', time=current_time, server_url=server_url)

1. 并且发送了time和server_url变量给页面使用,使用方法{{variable}}

1. 装饰器

1. before_request

1. 作用：用来获取request请求信息

1. 使能跨域请求

1. 安装：pip install flask-cors

1. 使用

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # 启用 CORS，允许所有来源的跨域请求
```

1. paramiko:通过ssh协议来执行命令

1. pexpect：自动化本地执行命令

1. 注意：windows系统不支持，但是可以用winpexpect库替代

1. datetime

1. datetime：时间对象

1. now函数：可以得到当前系统时间

1. timedelta：时间差对象，可以和datetime对象做加减法得到新的时间

1. ctypes:

1. windll模块：可以加载dll库，调用windows底层API，具体API可以查阅Michrosoft官方文档

1. logging：python标准日志库

1. 帮助网站

1. syslog：只能在unix环境下使用的日志模块

1. 帮助网站

1. collections

1. OrderedDict：有序字典对象

1. namedtuple:一个工厂函数，用来创建具名元组

1. 示例

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])

# 创建一个 Point 对象
p = Point(1, 2)

# 通过名称访问
print(p.x)  # 输出: 1
print(p.y)  # 输出: 2

```

1. 1

```python

```

1. tabulate：将表格数据（通常是列表或者字典）以表格格式打印到控制台或者输出流中

1. DrissionPage：web自动化库

1. 库的常用类类型，可以通过DrissionPage.items导入

1. subprocess：用来创建子进程，并可以连接他们的input/output/error通道，并获取他们的返回码

1. 常用函数

1. subprocess.check_output():执行指定的命令，如果执行成功则返回状态码，否则抛出异常，其功能等价于subprocess.run(…, check=True)。

1. subprocess.run()：执行指定的命令

1. capture_output：为True表示捕获输出

1. argparse：可以用来添加参数

1. 创建对象

1. argparse.ArgumentParser()

1. 创建子命令集合

1. add_subparsers

1. 添加子命令到集合中

1. add_parser

1. 添加参数

1. add_argument()

1. 作用：添加单个命令参数

1. 参数解析

1. 选项/位置参数

1. 选项参数

1. 短选项

1. 长选项

1. --str1-str2解析之后的变量名为str1_str2

1. 位置参数

1. action

1. 'store'表示存储参数

1. 'store_const'表示赋值为const

1. 'store_true'表示给定了参数，参数值为true否则为false

1. help

1. 打印的帮助信息

1. 解析执行脚本时传入的命令行参数，并根据之前定义的参数规则生成相应的属性

1. parse_args()

1. 返回值的类成员名为选项名，值为选项的参数值

1. click：用来实现终端命令行的第三方库

1. 帮助网站：

1. 打印帮助信息

1. python xxx.py --help

1. 方法

1. click.get_current_context()

1. 作用：获取命令上下文

1. add_command(func name, cmd_name)

1. 作用：手动向组里关联命令

1. 装饰器

1. @click.pass_context

1. 作用

1. 把click的上下文对象注入函数

1. 即可以读写参数，共享数据，调用其他命令等

1. @click.argument('interfacename', required=False)

1. 作用：为命令添加一个位置参数

1. 参数解析

1. 'interfacename'：位置参数的名称

1. required：一个bool类型的变量，用于表示这个位置参数是否是必须的

1. @click.command()

1. 作用：把函数装饰成一个命令

1. @click.option("--count", default=1, help="Number of greetings.")

1. 作用：给定一个选项参数，不显示使用这个参数时，默认值为1，help为帮助信息（如果不加default，必须显示指定）

1. @click.option("--name", prompt="Your name", help='xxx')

1. 作用:给定一个选项参数，提示字符为Your name

1. 创建组

1. @click.group()

1. 作用：将一个普通函数转换为一个Click组对象

1. 可以添加子命令：

1. 通过.add_command()方法向组中添加子命令，子命令可以是其他使用@click.command()装饰的函数

1. 可以创建嵌套组，即一个组里可以包含其他组