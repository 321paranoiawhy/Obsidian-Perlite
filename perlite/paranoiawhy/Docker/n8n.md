# Local

## `Dockerfile`

```bash
docker build -t n8n .
```

```bash
docker run --name n8n -p 5678:5678 -p 443:443 -d n8n
```

### `Dockerfile` 配置:

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

> [!attention]
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

## `npm`

```bash
npm install -g lerna
npm install --production --loglevel notice
lerna bootstrap --hoist
npm run build
npm run start
```

### `sqlite3`

> [!error]
> Initializing n8n process
> There was an error initializing DB: "SQLite package has not been found installed. Try to install it: npm install sqlite3 --save"

```bash
npm install sqlite3 --save
```

```bash
npm i node-pre-gyp -g
```

- [node-pre-gyp 以及 node-gyp 的源码简单解析（以安装 sqlite3 为例）](https://juejin.cn/post/6949528268512952333)

> [!error]
> Error: There was an error: SQLITE_ERROR: no such column: WorkflowEntity.userId

### `host.docker.internal`

> [!danger]
> "Host 'host.docker.internal' is not allowed to connect to this MySQL server"

查询 `MySQL` 用户:

```sql
select Host, User from mysql.user;
```

# Official

## `npm`

- [npm](https://docs.n8n.io/hosting/installation/npm/)

```bash
npx n8n
```

本地打开链接 `http://localhost:5678/` 即可。

## `Docker`

- [Docker Installation](https://docs.n8n.io/hosting/installation/docker/)

```bash
docker run -it --rm	--name n8n -p 5678:5678	-v ~/.n8n:/home/node/.n8n	n8nio/n8n
```