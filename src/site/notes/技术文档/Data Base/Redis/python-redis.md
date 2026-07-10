---
{"dg-publish":true,"permalink":"/技术文档/Data Base/Redis/python-redis/","dg-note-properties":{}}
---

1. redis基本概念

1. 非关系型数据库（NoSQL，Not only SQL）

1. Redis数据模型

1. Redis是一种key-value的数据结构，每条数据都是一个键值对

1. 键的类型是字符串

1. 值的类型分为五种

1. String---字符串

1. Hash---哈希{key:value}

1. List---列表

1. set---集合

1. Zest---有序集合

1. redis-cli操作

1. 连接到redis服务器

1. 本地

1. redis-cli

1. 远程

1. redis-cli -h host -p port -a password

1. 查看数据库的所有键

1. keys *

1. scan 0（游标）

1. 选择数据库（通过索引，一般是0~15）

1. select <索引>

1. 查看某一个键是否存在，并输出这个键值的类型

1. exists key_name

1. type key_name

1. 创建 or 修改

1. hash键值

1. redis-cli hset hash_key field value

1. 删除

1. redis-cli del hash_key

1. 删除hash字段

1. redis-cli hdel hash_key field_name

![](/img/user/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/Data%20Base/Redis/images/WEBRESOURCE36db37c325fec1607f07a54104ccfed2image.png)

1. 库的安装

1. pip install redis

1. 库的使用

1. StrictRedis(db = db_id, redis_kwargs)

1. db_id：指定要使用的Redis数据库的编号（默认情况下是16个）

1. redis_kwargs: 包含了除了db之外的其他关键字参数

1. 例如

```python
redis_kwargs = {
    'host': 'localhost',
    'port': 6379,
    'password': 'your_password'
}
db = redis.StrictRedis(db=0, **redis_kwargs)
```

1. client.config_set('notify-keyspace-events', self.KEYSPACE_EVENTS)

1. 作用：启用键空间通知（允许客户端订阅Redis数据库中的特定类型事件，如键的设置、删除等）

1. client.hget(name, key)

1. 参数含义

1. name：哈希表的名称，即redis中的键

1. key是你想要检索的字段名

1. client.hset(name, key, val)

1. 参数含义

1. name：哈希表的名称，即redis中的键

1. key是你想要设置的字段名

1. val是对应字段名的值