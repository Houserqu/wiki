# Redis

[Redis 简介](https://www.bookstack.cn/read/redis-tutorial/0.md)

## 命令

```jsx
> redis-cli -h {ip} -a {password} // 登录
```

## 数据库

redis 默认有16个数据库，不能自定义名称，而且共用同一个密码，数据库之间不是完全隔离的，FLUSHALL可以清空所有数据库。

所以如果有多个应用需要使用 redis，通过不同实例来实现，一个实例一个配置文件，可以配置端口、名称、密码

[参考](https://www.cnops.xyz/archives/996)

## 数据类型

![picture 28](../../images/1fe077fc9f0302e87ccc87456a1e60d33a47100e746e15371ac5bacfca425ddb.png)  

## 发布订阅

## JSON

redis 默认只能存储文本数据，但是可以通过 RedisJSON 模块实现直接存储/读取 json 数据
[https://hub.docker.com/r/redislabs/rejson/](https://hub.docker.com/r/redislabs/rejson/)