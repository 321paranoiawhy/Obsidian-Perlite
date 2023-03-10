# 单独运行

## 构建镜像

```bash
docker build -t backend-api-device .
```

## 运行

```bash
docker run --name backend-api-device -p 1235:8080 -d backend-api-device
```

# docker-compose

`docker-compose.yml` :

```yml
version: '3'

services:
  # redis
  redis:
    image: redis:alpine
  # go
  go:
    build: .
    ports:
      - "1235:8080"
    environment:
      # - REDIS_ADDR=http://10.10.21.86:6379
      - REDIS_ADDR=redis:6379
      - REDIS_DB=2
    depends_on:
      - redis
```

## 运行

```bash
docker-compose up
```