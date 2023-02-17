#Docker #docker-logs
# 语法

```bash
docker logs [OPTIONS] CONTAINER
```

# 查看输出详情

```bash
docker logs --detail CONTAINER
```

# 实时查看输出

```bash
docker logs -f CONTAINER
```

> [!tip]
> `-f` / `--folow` 均可。

# 查看某一时刻以后的输出

```bash
docker logs --since="2013-01-02T13:23:37Z" CONTAINER
docker logs --since 2013-01-02T13:23:37Z CONTAINER
```

# 查看某一时刻以前的输出

```bash
docker logs --until="2013-01-02T13:23:37Z" CONTAINER
docker logs --until 2013-01-02T13:23:37Z CONTAINER
```

# 仅查看最新的 `N` 条输出

仅查看最新的 `10` 条输出:

```bash
docker logs --tail=10 CONTAINER
```

> [!tip]
> `--tail` / `-n` 均可。

# Reference

- [docker logs - docker docs](https://docs.docker.com/engine/reference/commandline/logs/)