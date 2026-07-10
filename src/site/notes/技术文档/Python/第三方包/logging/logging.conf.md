---
{"dg-publish":true,"permalink":"/技术文档/Python/第三方包/logging/logging.conf/","dg-note-properties":{}}
---

1. 通过json配置文件配置

1. 加载配置字典API

1. logging.conf.dictConfig()

1. 字典架构

1. 引用内部对象要特殊标记

1. 例如："stream": "ext://sys.stdout"

1. 用户定义对象（可作为处理器、过滤器、格式化器，不支持日志记录器）

1. 键为：对象ID，值为：dict()

1. 键为（），值为str：一个类类型

1. 键为类参数名：值为：参数值

1. 注意：参数名和参数值会原样传入类的初始化函数中

1. 特殊键：'.'：其值为一个字典，用来更改创建的对象的属性值

1. 示例

```python
{
  '()' : 'my.package.customFormatterFactory',
  'bar' : 'baz',
  'spam' : 99.9,
  'answer' : 42,
  '.' {
    'foo': 'bar',
    'baz': 'bozz'
  }
}
```

1. 必须包含的键

1. version

1. value=1，唯一有效值

1. 可选键

1. formatters

1. value=dict(), 字典的每个键都是一个格式器ID

1. value=dict(), 描述如何配置相应的格式器，这些键对应创建Formatter对象时传入的参数

1. format

1. datefmt

1. style

1. validate

1. defaults

1. handlers

1. 配置对应处理器对象参数

1. class(强制)：处理器类的完整限定名称，即类类型

1. level(): 处理器的级别

1. formatter(可选): c处理器所对应格式器的ID

1. filters(可选): 由处理器所对应过滤器的ID组成的列表

1. filters

1. disable_existing_loggers

1. 一个bool类型的值用来确定是否禁用已经存在的日志记录器

1. loggers

1. 配置对应记录器对象参数

1. level

1. propagate

1. filters

1. handlers：一个列表

1. 示例

```python
{
    "version": 1,
    "disable_existing_loggers": false,
    "formatters": {
      "default": {
        "format": "[%(asctime)s][%(levelname)s]%(message)s",
        "datefmt": "%y/%m/%d %H:%M:%S"
      }
    },
    "handlers": {
      "file_handler": {
        "class": "logging.handlers.RotatingFileHandler",
        "level": "DEBUG",
        "formatter": "default",
        "filename": "app.log",
        "maxBytes": 10485760,
        "backupCount": 5
      },
      "stream_handler": {
        "class": "logging.StreamHandler",
        "level": "DEBUG",
        "formatter": "default"
      }
    },
    "loggers": {
      "default_logger": {
        "level": "DEBUG",
        "handlers": ["file_handler", "stream_handler"]
      }
    }
  }
  
```