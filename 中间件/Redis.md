## 安装

1. brew install redis
2. docker run --name redis-dev -v /data/home/houserqu/redis/dev-conf:/usr/local/etc/redis -d -p 6381:6379 redis
3. 使用自定义配置文件
   docker run --name redis-dev -v /home/houserqu/redis:/usr/local/etc/redis -d -p8079:6379 redis:bullseye redis-server /usr/local/etc/redis/redis.conf

## 配置

允许远程登录的配置

```
protected-mode no
bind [0.0.0.0](http://0.0.0.0)
requirepass 382027881
```