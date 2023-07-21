# Local

## Dockerfile

```bash
docker build -t n8n .
```

```bash
docker run --name n8n -p 5678:5678 -p 443:443 -d n8n
```

### Dockerfile 配置

```dockerfile
# packages/cli/config/index.ts
ENV DB_MYSQLDB_HOST=10.10.21.86
ENV DB_MYSQLDB_PORT=3307
ENV DB_MYSQLDB_USER=root
ENV DB_MYSQLDB_PASSWORD=123456
ENV QUEUE_BULL_REDIS_HOST=10.10.21.86
ENV QUEUE_BULL_REDIS_PORT=6379
ENV QUEUE_BULL_REDIS_PASSWORD=''

# packages/nodes-base/config/index.ts
ENV STORAGE_REDIS_HOST=10.10.21.86
ENV STORAGE_REDIS_PORT=6379
```

> [!caution]
> `MySQL` 中须有 `n8n` 数据表。

`packages/nodes-base/config/index.ts` :

```ts
STORAGE_REDIS_HOST: process.env.STORAGE_REDIS_HOST ?? '10.10.21.86',
STORAGE_REDIS_PORT: process.env.STORAGE_REDIS_PORT ?? '6379',
```

> [!tip]
> 关于 `process.env` :
> - [process.env - node.js](https://nodejs.org/dist/latest-v8.x/docs/api/process.html#process_process_env)
> - [来，让我们一起来盘盘 Nodejs 环境变量 (process.env)](https://juejin.cn/post/6915214622601674760)

## npm

```bash
npm install -g lerna
npm install --production --loglevel notice
node loadEnv.js
lerna bootstrap --hoist
npm run build
npm run start
```

> [!important] loadEnv.js
> ```js
> require('dotenv').config();
> console.log(process.env);
> ```

> [!success] lerna bootstrap --hoist
> lerna success Bootstrapped 6 packages

> [!success] npm run build
> lerna success exec Executed command in 6 packages: "npm run build"

> [!error] npm run start
> Initializing n8n process
> invalid vhost [].
>  »   Error: There was an error: Cannot read property 'on' of undefined

> [!error]
> There was an error initializing DB: "Access denied for user 'root'@'localhost' (using password: NO)"

查询 `MySQL` 用户:

```sql
select Host, User from mysql.user;
```

`powershell` :

```powershell
$env:DB_MYSQLDB_DATABASE="n8n";$env:DB_MYSQLDB_HOST="localhost";$env:DB_MYSQLDB_PORT="3307";$env:DB_MYSQLDB_USER="root";$env:DB_MYSQLDB_PASSWORD="123456";$env:DB_TYPE="mysqldb";$env:PORTAL_API_BASE="http://api-portal:8080";$env:DEVICE_API_BASE="http://api-device:8080";$env:DEVICE_DATA_API_BASE="http://api-data:8080";$env:VIRTUAL_CONTROLLER_API_BASE="http://api-virtual-controller:5000";$env:MQTT_PROTOCOL="mqtt";$env:MQTT_HOST="localhost";$env:MQTT_PORT="1883";$env:MQTT_CLEAN_SESSION="false";$env:RABBITMQ_URLS="amqp://localhost:5672/";$env:RABBITMQ_MESSAGE_QUEUE_VHOST="n8n-mq";$env:RABBITMQ_USERNAME="guest";$env:RABBITMQ_PASSWORD="guest";$env:RABBITMQ_TOPIC_EXCHANGENAME="amq.topic";$env:RABBITMQ_TRIGGER_QUEUE_TTL="300000";$env:RABBITMQ_QUEUENAME_WEBSOCKET_DATA="cereb.websocket-data";$env:SHADOW_WEBSOCKET_TOPIC="/topic/shadow_websocket";$env:STORAGE_REDIS_HOST="localhost";$env:STORAGE_REDIS_PORT="6379";$env:STORAGE_REDIS_DB="1";$env:REDIS_CACHE_DEVICE_TIME_SEC="600";$env:QUEUE_BULL_REDIS_HOST="localhost";$env:QUEUE_BULL_REDIS_PORT="6379";$env:QUEUE_BULL_REDIS_DB="1";$env:EXECUTIONS_PROCESS="own";$env:EXECUTIONS_MODE="regular";$env:N8N_SKIP_WEBHOOK_DEREGISTRATION_SHUTDOWN="false";$env:WEBHOOK_DOMAIN="localhost:5678/";$env:WORKFLOW_DOMAIN="localhost:5678/";$env:WEBHOOK_URL="http://localhost:5678/";$env:CUSTOM_BASE_URL="http://localhost:5678/";$env:N8N_DISABLE_PRODUCTION_MAIN_PROCESS="true";$env:N8N_BASIC_AUTH_ACTIVE="false";$env:N8N_HOST="localhost";$env:N8N_PORT="5678";$env:N8N_PROTOCOL="http";$env:N8N_CEREB_JWT_SECRET="cerebsecret";$env:N8N_ENCRYPTION_KEY="itsn8nsecret";$env:VUE_APP_URL_BASE_API="http://localhost:5678/";$env:NODE_ENV="production";$env:EXECUTIONS_DATA_PRUNE="true";$env:EXECUTIONS_DATA_MAX_AGE="168";$env:EXECUTIONS_TIMEOUT_MAX="600"
```



```powershell
$env:DB_MYSQLDB_DATABASE="n8n";$env:DB_MYSQLDB_HOST="localhost";$env:DB_MYSQLDB_PORT="3307";$env:DB_MYSQLDB_USER="root";$env:DB_MYSQLDB_PASSWORD="123456";$env:DB_TYPE="mysqldb";$env:PORTAL_API_BASE="http://api-portal:8080";$env:DEVICE_API_BASE="http://api-device:8080";$env:DEVICE_DATA_API_BASE="http://api-data:8080";$env:VIRTUAL_CONTROLLER_API_BASE="http://api-virtual-controller:5000";$env:MQTT_PROTOCOL="mqtt";$env:MQTT_HOST="localhost";$env:MQTT_PORT="1883";$env:MQTT_CLEAN_SESSION="false";$env:RABBITMQ_URLS="amqp://localhost:5672/";$env:RABBITMQ_MESSAGE_QUEUE_VHOST="n8n-mq";$env:RABBITMQ_USERNAME="guest";$env:RABBITMQ_PASSWORD="guest";$env:RABBITMQ_TOPIC_EXCHANGENAME="amq.topic";$env:RABBITMQ_TRIGGER_QUEUE_TTL="300000";$env:RABBITMQ_QUEUENAME_WEBSOCKET_DATA="cereb.websocket-data";$env:SHADOW_WEBSOCKET_TOPIC="/topic/shadow_websocket";$env:STORAGE_REDIS_HOST="localhost";$env:STORAGE_REDIS_PORT="6379";$env:STORAGE_REDIS_DB="1";$env:REDIS_CACHE_DEVICE_TIME_SEC="600"
```

在 `powershell` 中输入 `env.ps1` 后报错如下:

> [!error]
> Suggestion [3,General]: 找不到命令 env.ps1，但它确实存在于当前位置。默认情况下，Windows PowerShell 不会从当前位置加载命令。如果信任此命令，请改为键入“.\env.ps1”。有关详细信息，请参阅 "get-help about_Command_Precedence"。

在 `powershell` 中输入 `.\env.ps1` 即可:

```bash
.\env.ps1
```

- [Execution modes and processes - n8n Documentation](https://docs.n8n.io/hosting/scaling/execution-modes-processes/)
- `EXECUTIONS_PROCESS` : `own (default)` 或 `main` 
- `EXECUTIONS_MODE` : `regular (default)` 或 `queue`

`cmd` :

> [!tip]- /healthz [GET]
> ```ts
> 		// ----------------------------------------
> 		// Healthcheck
> 		// ----------------------------------------
> 
> 
> 		// Does very basic health check
> 		this.app.get('/healthz', async (req: express.Request, res: express.Response) => {
> 
> 			// const connectionManager = getConnectionManager();
> 
> 			// if (connectionManager.connections.length === 0) {
> 			// 	const error = new ResponseHelper.ResponseError('No Database connection found!', undefined, 503);
> 			// 	return ResponseHelper.sendErrorResponse(res, error);
> 			// }
> 
> 			// if (connectionManager.connections[0].isConnected === false) {
> 			// 	// Connection is not active
> 			// 	const error = new ResponseHelper.ResponseError('Database connection not active!', undefined, 503);
> 			// 	return ResponseHelper.sendErrorResponse(res, error);
> 			// }
> 
> 			// Everything fine
> 			const responseData = {
> 				status: 'ok',
> 			};
> 
> 			ResponseHelper.sendSuccessResponse(res, responseData, true, 200);
> 		});
> ```

# Official

## npm

- [npm](https://docs.n8n.io/hosting/installation/npm/)

```bash
npx n8n
```

本地打开链接 `http://localhost:5678/` 即可。

## Docker

- [Docker Installation](https://docs.n8n.io/hosting/installation/docker/)

```bash
docker run -it --rm	--name n8n -p 5678:5678	-v ~/.n8n:/home/node/.n8n	n8nio/n8n
```


# 本地开发调试

```bash
npm install -g lerna
npm install --production --loglevel notice
.\env.ps1
lerna bootstrap --hoist
npm run build
npm run start
```

> [!tip]- env.ps1
> ```powershell
> $env:DB_MYSQLDB_DATABASE="n8n"
> $env:DB_MYSQLDB_HOST="localhost"
> $env:DB_MYSQLDB_PORT="3307"
> $env:DB_MYSQLDB_USER="root"
> $env:DB_MYSQLDB_PASSWORD="123456"
> $env:DB_TYPE="mysqldb"
> $env:PORTAL_API_BASE="http://api-portal:8080"
> $env:DEVICE_API_BASE="http://api-device:8080"
> $env:DEVICE_DATA_API_BASE="http://api-data:8080"
> $env:VIRTUAL_CONTROLLER_API_BASE="http://api-virtual-controller:5000"
> $env:MQTT_PROTOCOL="mqtt"
> $env:MQTT_HOST="localhost"
> $env:MQTT_PORT="1883"
> $env:MQTT_CLEAN_SESSION="false"
> $env:RABBITMQ_URLS="amqp://localhost:5672/"
> $env:RABBITMQ_MESSAGE_QUEUE_VHOST="n8n-mq"
> $env:RABBITMQ_USERNAME="guest"
> $env:RABBITMQ_PASSWORD="guest"
> $env:RABBITMQ_TOPIC_EXCHANGENAME="amq.topic"
> $env:RABBITMQ_TRIGGER_QUEUE_TTL="300000"
> $env:RABBITMQ_QUEUENAME_WEBSOCKET_DATA="cereb.websocket-data"
> $env:SHADOW_WEBSOCKET_TOPIC="/topic/shadow_websocket"
> $env:STORAGE_REDIS_HOST="localhost"
> $env:STORAGE_REDIS_PORT="6379"
> $env:STORAGE_REDIS_DB="1"
> $env:REDIS_CACHE_DEVICE_TIME_SEC="600"
> ```

设置环境变量:

- `win + r` 后输入 `sysdm.cpl` 选择**高级选项卡** -> **环境变量**
- `win + s` 后输入**环境变量** 选择**编辑系统环境变量**
- `cmd` 下 `set test='test'`
- `powershell` 下 `$env:test='test'`
- `bash` 或 `zsh` 下 `export test=test`

查看 `bash` 还是 `zsh` :

```bash
echo $0
echo $SHELL
```