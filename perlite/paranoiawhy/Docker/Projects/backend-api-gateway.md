# 单独运行

## 构建镜像

```bash
docker build -t backend-api-gateway .
```

## 运行

```bash
docker run --name backend-api-gateway -p 1236:8080 -d backend-api-gateway
```

# `docker-compose`

`docker-compose.yml` :

```yml
version: '3'

services:
  # redis
  redis:
    image: redis:alpine
  # java
  java:
    build: .
    ports:
      - "1236:8080"
    environment:
      - AUTH_SERVICE_URL=http://api-auth-center:8080
      - PORTAL_SERVICE_URL=http://api-portal:8080
      - VIRTUAL_CONTROLLER_URL=http://api-virtual-controller:5000
      - SALTO_INTEGRATION_SERVICE_URL=http://integration-salto:5000
      - UHOO_INTEGRATION_SERVICE_URL=http://integration-uhoo:5000
      - LIFESMART_INTEGRATION_SERVICE_URL=http://integration-lifesmart:5000
      - COOLAUTOMATION_INTEGRATION_SERVICE_URL=http://integration-coolautomation:5000
      - AIRTHINGS_INTEGRATION_SERVICE_URL=http://integration-airthings:5000
      - KUJU_INTEGRATION_SERVICE_URL=http://integration-kuju:5000
      - MOODO_INTEGRATION_SERVICE_URL=http://integration-moodo:5000
      - HUB_INTEGRATION_SERVICE_URL=http://integration-hub:5000
      - WEBSOCKET_TRANSMITTER_SERVICE_URL=http://api-portal:8080
      - WEBSOCKET_TRANSMITTER_SERVICE_WS_URL=ws://api-portal:8080
      - SECURITY_JWT_SECRET=1234
      - SPRING_REDIS_DATABASE=0
      - SPRING_REDIS_HOST=redis
      - SPRING_REDIS_PORT=6379
    depends_on:
      - redis
```

## 运行

```bash
docker-compose up
```