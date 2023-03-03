# 分别运行

## 启动前置依赖

`Maven` 安装依赖:

```bash
& mvn install -f "d:\work\backend\
```

> [!info]
> 本项目有三个前置依赖:
> - `redis`
> - `Rabbitmq`
> - `MySQL`

### `redis`

- [redis docker hub](https://hub.docker.com/_/redis)

启动 `redis` :

```bash
docker run --name redis -p 6379:6379 -d redis
```

### `Rabbitmq`

- [Rabbitmq - docker hub](https://hub.docker.com/_/rabbitmq)

启动 `Rabbitmq` :

```bash
docker run -d --hostname my-rabbit -p 5672:5672 --name some-rabbit rabbitmq:3
```

### `MySQL`

- [MySQL - docker hub](https://hub.docker.com/_/mysql)

启动 `MySQL` :

```bash
docker run --name some-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7
```

> [!important]
> - `redis` 默认端口号为 `6379`
> - `Rabbitmq` 默认端口号为 `5672`
> - `mysql` 默认端口号为 `3306`

## 在 `Dockerfile` 中配置环境变量

`k8s\deployment.yaml` :

```yml
containers:
      - env:
        - name: SPRING_REDIS_DATABASE
          value: "2"
        - name: SPRING_REDIS_HOST
          value: redis
        - name: SPRING_REDIS_PORT
          value: "6379"

        - name: SPRING_RABBITMQ_ADDRESSES
          value: "amqp://rabbitmq-server-0.rabbitmq-nodes:5672/,amqp://rabbitmq-server-1.rabbitmq-nodes:5672/,amqp://rabbitmq-server-2.rabbitmq-nodes:5672/"
        - name: SPRING_RABBITMQ_USERNAME
          value: cereb-user
        - name: SPRING_RABBITMQ_PASSWORD
          valueFrom:
            secretKeyRef:
              name: rabbitmq-secret
              key: cereb-user-password
        - name: RABBITMQ_TOPIC_EXCHANGENAME
          value: amq.topic

        - name: INFLUXDB_URL
          value: http://influxdb-0.influxdb:8086
        - name: INFLUXDB_TOKEN
          value: cereb-influx-token
        - name: INFLUXDB_ORG
          value: cereb-org
        - name: INFLUXDB_BUCKET
          value: device_data
        - name: LOGGING_LEVEL_COM_SQUARECOOKY
          value: debug
```

根据 `k8s\deployment.yaml` 中环境变量的设置相应的配置 `Dockerfile` 文件:

```dockerfile
FROM openjdk:8u131-jre-alpine

MAINTAINER Wu Pei Hong

ENV SPRING_REDIS_DATABASE="2"
ENV SPRING_REDIS_HOST=10.10.21.86
ENV SPRING_REDIS_PORT="6379"
ENV SPRING_RABBITMQ_ADDRESSES="amqp://10.10.21.86:5672/"

ENV SPRING_RABBITMQ_USERNAME=guest
ENV SPRING_RABBITMQ_PASSWORD=guest

ENV RABBITMQ_TOPIC_EXCHANGENAME=amq.topic
ENV INFLUXDB_URL=http://10.10.21.86:8086
ENV INFLUXDB_TOKEN=cereb-influx-token
ENV INFLUXDB_ORG=cereb-org
ENV INFLUXDB_BUCKET=device_data
ENV LOGGING_LEVEL_COM_SQUARECOOKY=debug

WORKDIR /usr/local/apps/cereb/

COPY ./target/backend-api-data-0.0.1-SNAPSHOT.jar ./data-0.1.jar

EXPOSE 8080

ENTRYPOINT exec java -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -jar data-0.1.jar
```

> [!important]
> 需将以下变量值中的地址更换为本机 `ip` (`10.10.21.86`) :
> - `SPRING_REDIS_HOST`
> - `SPRING_RABBITMQ_ADDRESSES`
> - `INFLUXDB_URL`
> 同时将 `SPRING_RABBITMQ_USERNAME` 和 `SPRING_RABBITMQ_PASSWORD` 的值均更改为 `guest`。

参考:
- [ENV 设置环境变量](https://yeasy.gitbook.io/docker_practice/image/dockerfile/env)

## 构建镜像

```bash
docker build -t backend-api-data .
```

> [!danger]
> 每次修改 `Dockerfile` 后都需要重新**构建镜像**后再将镜像**运行到容器**。
> 如果只重新运行到容器, 则 `Dockerfile` 的变更不会生效。

## 运行到容器

```bash
docker run --name backend-api-data -p 1234:8080 -d backend-api-data
```

> [!important]
> `1234:8080`
> - 冒号前面的 `1234` 表示使用的本地的端口为 `1234` 。
> - 冒号后面的 `8080` 须对应 `Dockerfile` 文件中 `EXPOSE` 的值, 这里即 `8080` 。

## 模拟请求

实际代码 `src\main\java\com\cereb\devicedata\controller\DeviceDataController.java` :

```java
@GetMapping("/data/devices/devices_batch/live")
List<DeviceData> queryLiveDataByBatch(@RequestParam String[] deviceKeys) {
	return deviceDataDao.queryLiveDataByBatch(deviceKeys);
}
```

- 模拟请求 `URL` : `http://localhost:1234/data/devices/devices_batch/live`
- 查询 `query` 参数名为 `deviceKeys` , 测试时参数值可任意, 如 `test`
- 返回结果:
```json
{
    "code": 100,
    "msg": "unknown error",
    "source": "api-data"
}
```

> [!tip]
> 也可在浏览器里直接输入链接 `http://localhost:1234/data/devices/devices_batch/live?deviceKeys=test` , 页面将显示上述 `json` 。

# `docker-compose`

```yml
version: '3'

services:
  # redis
  redis:
    image: "redis:alpine"

  # Rabbitmq
  Rabbitmq:
    image: "rabbitmq:3"

  # influxdb
  influxdb:
    image: "influxdb:2.3-alpine"

  # java
  java:
    build: .
    ports:
      - "1234:8080"
    environment:
      - SPRING_REDIS_DATABASE=2
      - SPRING_REDIS_HOST=10.10.21.86
      - SPRING_REDIS_PORT=6379
      - SPRING_RABBITMQ_ADDRESSES=amqp://10.10.21.86:5672/
      - SPRING_RABBITMQ_USERNAME=guest
      - SPRING_RABBITMQ_PASSWORD=guest
      - RABBITMQ_TOPIC_EXCHANGENAME=amq.topic
      - INFLUXDB_URL=http://10.10.21.86:8086
      - INFLUXDB_TOKEN=cereb-influx-token
      - INFLUXDB_ORG=cereb-org
      - INFLUXDB_BUCKET=device_data
      - LOGGING_LEVEL_COM_SQUARECOOKY=debug
    depends_on:
      - redis
      - Rabbitmq
      - influxdb
```

`docker-compose.yml` 文件中 `ip` (`10.10.21.86`) 可替换成相应的值:

```yml
SPRING_REDIS_HOST=redis
SPRING_RABBITMQ_ADDRESSES=amqp://Rabbitmq:5672/
INFLUXDB_URL=http://influxdb:8086
```

## 运行

```bash
docker-compose up
```

# `docker-rabbitmq-cluster`

- [Cluster RabbitMQ](https://github.com/pardahlman/docker-rabbitmq-cluster)

> [!info]
> docker-rabbitmq-cluster-rabbitmq2-1  | exec /usr/local/bin/cluster-entrypoint.sh: no such file or directory
> docker-rabbitmq-cluster-rabbitmq3-1  | exec /usr/local/bin/cluster-entrypoint.sh: no such file or directory
> docker-rabbitmq-cluster-rabbitmq1-1  | 2023-02-10 02:25:52.725516+00:00 [warning] <0.132.0> Overriding Erlang cookie using the value set in the environment
> docker-rabbitmq-cluster-rabbitmq2-1 exited with code 1
> docker-rabbitmq-cluster-rabbitmq3-1 exited with code 1

`cluster-entrypoint.sh` `Select End of Line Sequence` 由 `CRLF` 改为 `LF`

# `Clustering RabbitMQ Docker containers`

```bash
docker network create rabbitmq-cluster
```

```bash
docker-compose up
```

```bash
docker network ls
```

```bash
docker network rm
```

- [RabbitMQ-Docker-cluster - GitHub](https://github.com/MingxuanHu/RabbitMQ-Docker-cluster)
- [docker network create](https://docs.docker.com/engine/reference/commandline/network_create/)
- [docker network ls](https://docs.docker.com/engine/reference/commandline/network_ls/)
- [docker network rm](https://docs.docker.com/engine/reference/commandline/network_rm/)

> [!danger] MySQL
> [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
> You need to specify one of the following as an environment variable:
> - MYSQL_ROOT_PASSWORD
> - MYSQL_ALLOW_EMPTY_PASSWORD
> - MYSQL_RANDOM_ROOT_PASSWORD

## `MYSQL_ROOT_PASSWORD`

> [!quote]
> This variable is mandatory and specifies the password that will be set for the MySQL root superuser account. In the above example, it was set to my-secret-pw.

## `MYSQL_ALLOW_EMPTY_PASSWORD`

> [!quote]
> This is an optional variable. Set to a non-empty value, like yes, to allow the container to be started with a blank password for the root user. NOTE: Setting this variable to yes is not recommended unless you really know what you are doing, since this will leave your MySQL instance completely unprotected, allowing anyone to gain complete superuser access.

## `MYSQL_RANDOM_ROOT_PASSWORD`

> [!quote]
> This is an optional variable. Set to a non-empty value, like yes, to generate a random initial password for the root user (using pwgen). The generated root password will be printed to stdout (GENERATED ROOT PASSWORD: .....).


## `Rabbitmq` 插件

`Enable-Rabbitmq-Plugins-Dockerfile` :

```
FROM rabbitmq:3.8-management
RUN rabbitmq-plugins enable rabbitmq_mqtt rabbitmq_federation_management rabbitmq_stomp
```

由上述 `Enable-Rabbitmq-Plugins-Dockerfile` 文件构建带插件的 `Rabbitmq` 镜像 `rabbitmq_with_plugins` :

```bash
docker build -f Enable-Rabbitmq-Plugins-Dockerfile -t rabbitmq_with_plugins .
```

## `MySQL`

- [MySQL Community Server Download](https://downloads.mysql.com/archives/community/)
- `5.7.10`
- [MySQL 下载与安装](https://zhuanlan.zhihu.com/p/81801548)

配置 `MySQL` 环境变量:
- `MYSQL_HOME` : `D:\Software\mysql-5.7.10-winx64`
- `path` : 新增 `%MYSQL_HOME%\bin`

输入 `root` 用户密码:

```bash
mysql -u root -p
```

```bash
Enter password: ****
```