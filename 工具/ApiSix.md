> nginx 的增强版，支持web控制台

## 安装

### yum 安装

> yum 安装以来 etcd 和 nginx，不推荐

```bash
sudo yum install -y https://repos.apiseven.com/packages/centos/7/x86_64/apisix-2.11.0-0.el7.x86_64.rpm
sudo yum-config-manager --add-repo https://repos.apiseven.com/packages/centos/apache-apisix.repo
# View the information of the latest apisix package
sudo yum info -y apisix

# Will show the existing apisix packages
sudo yum --showduplicates list apisix

# Will install the latest apisix package
sudo yum install apisix

apisix init
```

### 注意点： 

apisix 部署在容器环境，所以配置上游服务 ip 用 [172.17.0.1](http://172.17.0.1) 

公网接口通过域名匹配 非公网普通接口通过使用 key-auth 鉴权