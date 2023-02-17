# `restart` 策略

## `Version 2`

- `restart: no` : 默认策略, 容器只会启动一次, 即使启动失败也不会自动重启;
- `restart: alaways` : 容器启动失败后始终自动重启
- `restart: on-failure` : 退出码非 `0` 时容器自动重启, 如 `Exit(1)`
- `restart: unless-stopped` : 容器停止时自动重启
- [restart - docker docs](https://docs.docker.com/compose/compose-file/compose-file-v2/#restart)

## `Version 3`

- [restart_policy - docker docs](https://docs.docker.com/compose/compose-file/compose-file-v3/#restart_policy)