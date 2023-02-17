# 启动

```bash
docker network ls
```

```bash
docker network create rabbitmq-cluster
```

```bash
docker build -f Enable-Rabbitmq-Plugins-Dockerfile -t rabbitmq_with_plugins .
```

实时打印消息:

```bash
docker-compose up
```

不实时打印消息:

```bash
docker-compose up -d
```

# 本地连接至 `Docker` 中的 `MySQL`

## `docker run`

```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3310:3306 -d mysql:5.7
```

```bash
mysql -h localhost -P 3310 -u root

# mysql -P 3310 --protocol=tcp -u root -p
```

## `docker-compose`

```bash
mysql -P 3307 --protocol=tcp -u root -p
```

## 获取容器 `ip`

```bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id
```


