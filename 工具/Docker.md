

# Docker

## 文档

[Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/)

宿主访问容器

[http://www.louisvv.com/archives/695.html](http://www.louisvv.com/archives/695.html)

网络模式介绍

[https://juejin.im/post/6844903756920782855](https://juejin.im/post/6844903756920782855)

compose 的网络介绍比较详细

[https://michael728.github.io/2019/06/15/docker-compose-networks/](https://michael728.github.io/2019/06/15/docker-compose-networks/)

## 基础

### 网络

通过 docker network 创建自定义网络的时候，该网络下容器 expose 的端口跟默认的 bridge0 网络下的容器 expose 端口是在同一个宿主网络中，依然会冲突，访问容器的方式跟默认网桥也相同，只是内部容器的网络是隔离的

### docker-自动重启

![middle_img_v2_ab631234-0fdd-4144-b1da-6e16064c432g](http://qiniu.houserqu.com/middle_img_v2_ab631234-0fdd-4144-b1da-6e16064c432g-huqNDf.png)

```
一般建议使用 unless-stopped 策略
示例：docker run -d --restart unless-stopped tomcat
```

## 常用命令

![picture 17](../../images/dff5e78ebb792c1e03890cc779941909e8802530df5df931fe19b6a8eb3c3748.png)  

### 根据 Dockerfile 构建镜像

```bash
# 根据当前目录下的 Dockerfile 文件构建 tag 为 app/user、镜像
docker build -t app:1.0 .
```

###  容器操作

```bash
# 后台启动容器，并随机映射端口
docker run -it -P trpc-txcz-demo:0.2.0

# 后台启动容器，并挂载目录、映射端口、指定容器名称
docker run -d -p 8010:80 -v /www/wwwroot/api2.dongfanlaoshi.com/app/:/app --name dongfan2-2-api go-runner:latest
```

## docker-compose

### 网络

通过 docker-compose 启动的容器，容器之间访问直接用服务名称作为 host 进行互相访问，如访 mysql，`mysql:3306`

### 操作

```bash
# 指定配置文件并在后台启动容器
docker-compose -f "docker-compose.yml" up -d

# 停止所有容器
docker-compose -f "docker-compose.yml" stop

# 停止并删除所有容器
docker-compose -f "docker-compose.yml" down
```

### 进入容器

```bash
docker exec -it {id} bash # 如果 bash 不成功，可替换为 /bin/bash；exit 退出，容器不会停止
docker attach {id} # exit 后容器会停止
```

## 容器与宿主机访问

### 容器访问宿主机

- host.docker.internal 通过该域名直接访问（18.03版本后）
- 宿主机的 docker0 的 ip 访问（mac/win 不支持，查看方式:宿主机执行 ifconfig）
- host 网络模式直接访问（mac/win不支持）

### 宿主机访问容器

- expose 端口映射
- localhost:端口直接访问（network 为 host 模式才支持）