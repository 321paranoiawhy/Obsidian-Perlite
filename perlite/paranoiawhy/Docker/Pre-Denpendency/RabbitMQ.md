# 在 Docker 中运行

- [RabbitMQ](https://hub.docker.com/_/rabbitmq)

```bash
docker run -d --hostname my-rabbit --name some-rabbit rabbitmq:3
```

上述命令未暴露端口和映射关系, 可通过如下命令实现:

```bash
docker run -d --hostname my-rabbit -p 5672:5672 --name some-rabbit rabbitmq:3
```

# 报错

> [!error]
> Cookie file /var/lib/rabbitmq/.erlang.cookie must be accessible by owner only

- [rabbitmq 启动报错](https://blog.csdn.net/qq_35720307/article/details/103313655)