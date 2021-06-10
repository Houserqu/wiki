# PM2

## 示例

npm 启动脚本

```
 "start": "npm run build && pm2 start process.json --only 2b-tools"
```

Pm2 配置文件 process.json

```json
{
  "apps": [{
    "name": "2b-tools",
    "script": "./dist/server/server.js",
    "env_production" : {
      "NODE_ENV": "production"
    },
    "min_uptime": "60s",
    "max_restarts": 30,
    "log_date_format": "YYYY-MM-DD HH:mm Z",
    "error_file" : "./logs/pm2-err.log",
    "out_file"   : "./logs/pm2-out.log",
    "watch": false,
    "env": {
      "NODE_ENV": "production"
    },
    "node_args": ["--harmony"]
  }]
}
```