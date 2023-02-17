#Docker 
# 验证 `docker-compose.yml` 文件

验证 `docker-compose.yml` 文件格式是否正确, 若格式正确则显示配置内容, 反之则显示错误原因:

```bash
docker-compose config
```

> [!info]- docker-compose config
> name: backend-project-kt6562
> services:
>   python:
>     build:
>       context: D:\work\backend\backend-project-kt6562
>       dockerfile: Dockerfile
>     depends_on:
>       redis:
>         condition: service_started
>     environment:
>       REDIS_URL: redis://10.10.21.86:6379
>     networks:
>       default: null
>     ports:
>     - mode: ingress
>       target: 8080
>       published: "8080"
>       protocol: tcp
>   redis:
>     image: redis:alpine
>     networks:
>       default: null
> networks:
>   default:
>     name: backend-project-kt6562_default

验证 `docker-compose.yml` 文件格式是否正确, 仅格式错误时显示错误原因:

```bash
docker-compose config -q
```

# 启动

```bash
docker-compose up
```

> [!info] docker-compose up
> [+] Running 3/3
>  - Network backend-project-kt6562_default     Created                                                                                                                    0.0s 
>  - Container backend-project-kt6562-redis-1   Created                                                                                                                    0.1s 
>  - Container backend-project-kt6562-python-1  Created                                                                                                                    0.1s 
> Attaching to backend-project-kt6562-python-1, backend-project-kt6562-redis-1

# 暂停

```bash
docker-compose pause
```

可通过如下命令重新启动容器:

```bash
docker-compose unpause
```

> [!tip]
> `pause` 和 `unpause` 相辅相成。

# 停止

```bash
docker-compose stop
```

可通过如下命令重新启动容器:

```bash
docker-compose start
```

> [!tip]
> `stop` 和 `start` 相辅相成。

# 终止

终止 `docker-compose up` 命令所启动的容器 (`Container`) , 并移除网络 (`Network`)

```bash
docker-compose down
```

> [!info] docker-compose down
> [+] Running 3/3
>  - Container backend-project-kt6562-python-1  Removed                                                                                                                    0.4s 
>  - Container backend-project-kt6562-redis-1   Removed                                                                                                                    0.5s
>  - Network backend-project-kt6562_default     Removed

> [!tip]
> `up` 和 `down` 相辅相成。

# 列出 `docker-compose` 所有容器

```bash
docker-compose ps
```

# 查看输出

```bash
docker-compose logs
```

> [!tip]
> `-f` / `--follow` 可实时查看输出:
> 
> ```bash
> docker-compose logs -f
> ```

- [[Docker Commands/docker logs]]
- [docker compose logs](https://docs.docker.com/engine/reference/commandline/compose_logs/)