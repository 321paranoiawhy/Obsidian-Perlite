# RabbitMQ

- [RabbitMQ-Docker-cluster](https://github.com/MingxuanHu/RabbitMQ-Docker-cluster)

# zookeeper

- [docker-zookeeper](https://github.com/acntech/docker-zookeeper)
- [acntechie/zookeeper - docker hub](https://hub.docker.com/r/acntechie/zookeeper)

> [!tip]- docker-compose.yml
> ```yml
> version: "2"
> 
> services:
>   zookeeper1:
>     image: acntechie/zookeeper
>     container_name: zookeeper1
>     ports:
>       - "2181:2181"
>     environment:
>       - ZOOKEEPER_ID=1
>       - ZOOKEEPER_HOSTS=zookeeper1:2888:3888,zookeeper2:2888:3888,zookeeper3:2888:3888
>     networks:
>     - zookeeper-cluster
> 
>   zookeeper2:
>     image: acntechie/zookeeper
>     container_name: zookeeper2
>     ports:
>       - "2182:2181"
>     environment:
>       - ZOOKEEPER_ID=2
>       - ZOOKEEPER_HOSTS=zookeeper1:2888:3888,zookeeper2:2888:3888,zookeeper3:2888:3888
>     networks:
>     - zookeeper-cluster
> 
>   zookeeper3:
>     image: acntechie/zookeeper
>     container_name: zookeeper3
>     ports:
>       - "2183:2181"
>     environment:
>       - ZOOKEEPER_ID=3
>       - ZOOKEEPER_HOSTS=zookeeper1:2888:3888,zookeeper2:2888:3888,zookeeper3:2888:3888
>     networks:
>     - zookeeper-cluster
> 
> networks:
>   zookeeper-cluster:
> ```

创建网络 `zookeeper-cluster` :

```bash
docker network create zookeeper-cluster
```

```
docker-compose up -d
```

# Warning

> [!warning]
> network default: network.external.name is deprecated. Please set network.name with external: true

```yml
networks:
  default:
    external:
      name: cluster
```

改为:

```yml
networks:
  default:
    name: cluster
    external: true
```

或:

```yml
networks:
  cluster:
    external: true
```

- [Correct Syntax](https://github.com/docker/compose-cli/issues/1856#issuecomment-1108552064)