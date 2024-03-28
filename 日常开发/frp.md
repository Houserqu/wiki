内网穿透工具

https://github.com/fatedier/frp



### 我的frp使用方法

#### 在公网服务器启动服务端

在 8.142.23.228 机器上的 /home/frp/frp_0.53.2_linux_amd64 目录执行

```
./frps -c ./frps.toml
```

#### 在本地服务上启动客户端

在 /Users/houser/projects/frp/frp_0.53.2_darwin_arm64 目录执行

```
./frpc -c frpc.toml
```

端口配置见 frpc.toml 文件

配置示例

```
serverAddr = "124.128.90.165"
serverPort = 7000
auth.token = "daanjiexi"

[[proxies]]
name = "test-tcp"
type = "tcp"
localIP = "127.0.0.1"
localPort = 7100   # 8000 等特殊端口无效
remotePort = 7100  # 服务端开放的端口范围 7000-8000
```

