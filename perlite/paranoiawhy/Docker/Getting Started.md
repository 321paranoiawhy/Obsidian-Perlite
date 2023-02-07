#Docker #Getting-Started
# 运行 `docker`

> [!quote]
> `Build once, run everywhere`

> [!failure]
> Update the WSL kernel by running "wsl --update" or follow instructions at [here](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)

```bash
wsl --update
```

> [!info]
> 正在安装: 适用于 Linux 的 Windows 子系统
> 已安装 适用于 Linux 的 Windows 子系统。

# 查看 `docker` 版本

## `docker version`

```bash
docker version
```

> [!tip]- docker version
> Client:
>  Cloud integration: v1.0.29
>  Version:           20.10.22
>  API version:       1.41
>  Go version:        go1.18.9
>  Git commit:        3a2c30b
>  Built:             Thu Dec 15 22:36:18 2022
>  OS/Arch:           windows/amd64
>  Context:           default
>  Experimental:      true
>
> Server: Docker Desktop 4.16.3 (96739)
>  Engine:
>   Version:          20.10.22
>   API version:      1.41 (minimum version 1.12)
>   Go version:       go1.18.9
>   Git commit:       42c8b31
>   Built:            Thu Dec 15 22:26:14 2022
>   OS/Arch:          linux/amd64
>   Experimental:     false
>  containerd:
>   Version:          1.6.14
>   GitCommit:        9ba4b250366a5ddde94bb7c9d1def331423aa323
>  runc:
>   Version:          1.1.4
>   GitCommit:        v1.1.4-0-g5fd4c4d
>  docker-init:
>   Version:          0.19.0
>   GitCommit:        de40ad0

## `docker -v`

```bash
docker -v
```

> [!info] docker -v
> Docker version 20.10.22, build 3a2c30b

# 查看 `docker` 帮助

```bash
docker --help
```

```bash
docker sbom
```

- [Announcing Docker SBOM: A step towards more visibility into Docker images](https://www.docker.com/blog/announcing-docker-sbom-a-step-towards-more-visibility-into-docker-images/)

# `Tutorial`

## `docker run`

> [!note] docker run
> ```bash
> docker run --name repo alpine/git clone https://github.co
> ```

> [!info]
> m/docker/getting-started.git
> Unable to find image 'alpine/git:latest' locally
> ca7dd9ec2225: Pull complete
> eb878e0a08e4: Downloading  12.75MB/18.49MB
> b4f093b99828: Download complete
> ^C

## `docker cp`

> [!note] docker cp
> ```bash
> docker cp repo:/git/getting-started/ .
> ```
> - [docker cp](https://docs.docker.com/engine/reference/commandline/cp/)

> [!info]
> Error: No such container:path: repo:/git/getting-started/

# `docker search`

从 `https://hub.docker.com/` 上查询 `centos` 镜像是否存在:

```bash
docker search centos
```

![[../Attachments/docker-search-centos.png]]

拉取 `centos` 镜像

```bash
docker pull centos
```

# Getting Started

## 尝试运行

```bash
docker run -d -p 80:80 docker/getting-started
```

> [!info]
> ```bash
> Unable to find image 'docker/getting-started:latest' locally
> latest: Pulling from docker/getting-started
> c158987b0551: Pull complete
> 1e35f6679fab: Pull complete
> cb9626c74200: Pull complete
> b6334b6ace34: Pull complete
> f1d1c9928c82: Pull complete
> 9b6f639ec6ea: Pull complete
> ee68d3549ec8: Pull complete
> 33e0cbbb4673: Pull complete
> 4f7e34c2de10: Pull complete
> Digest: sha256:d79336f4812b6547a53e735480dde67f8f8f7071b414fbd9297609ffb989abc1
> Status: Downloaded newer image for docker/getting-started:latest
> ```

`docker` 在运行前会检查已有的镜像缓存, 如果镜像缓存中已存在该镜像, 则不拉取, 否则先拉取该镜像。

> [!hint]
> 这是由于 `docker` 的 `--pull` 默认值为 `missing`, [参见](https://docs.docker.com/engine/reference/commandline/run/#pull)
> `--pull` 的枚举值为:
> - `missing` (default)
> - `never`
> - `always`

## 查看所有已安装的镜像:

```bash
docker images
```

> [!info]
> ```bash
> REPOSITORY               TAG       IMAGE ID       CREATED       SIZE
> docker/getting-started   latest    3e4394f6b72f   6 weeks ago   47MB
> ```

重新运行 `docker run -d -p 80:80 docker/getting-started` 后提示 `Bind for 0.0.0.0:80 failed: port is already allocated.`:

> [!info]
> ```bash
> a1215e97a36cf0e74b82691b76896c6c7f67e153ce8db5b67ab2fcb8e65b1561
> docker: Error response from daemon: driver failed programming external connectivity on endpoint lucid_liskov (d91f26caf0ffc43582e0b07a140e08dca30f7748ac8e95794066c707e501319f): Bind for 0.0.0.0:80 failed: port is already allocated.
> ```

`Bind for 0.0.0.0:80 failed: port is already allocated.` 解决方法:

```bash
docker container ls
# 或者
docker ps
```

> [!info]
> ```bash
> CONTAINER ID   IMAGE                    COMMAND                  CREATED         STATUS         PORTS                NAMES
> fcc9c7b01999   docker/getting-started   "/docker-entrypoint.…"   5 minutes ago   Up 5 minutes   0.0.0.0:80->80/tcp   trusting_swanson
> ```

# `docker run` 参数

语法:

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

- [docker run](https://docs.docker.com/engine/reference/commandline/run/)

## `-d`

| --detach , -d | <span style="color: rgb(0, 0, 0); font-family: Roboto, sans-serif; font-size: 14px; background-color: rgb(247, 247, 247);">Run container in background and print container ID</span> |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

# `-p`

- [docker run --publish](https://docs.docker.com/engine/reference/commandline/run/#publish)

| --publish , -p | <span style="color: rgb(0, 0, 0); font-family: Roboto, sans-serif; font-size: 14px; background-color: rgb(247, 247, 247);">Publish a container's port(s) to the host</span> |
|:---------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

将本机 `80` 端口映射到 `docker container` `80` 端口:

```bash
docker run -p A:B
```

# 列出镜像

```bash
docker image ls
```

# 列出容器

## 列出运行中的所有容器

```bash
docker container ls
```

## 列出运行中和已终止的所有容器

```bash
docker ps -a
```

# 启动容器

> [!attention]
> 在启动容器之前, 请查看运行中和已终止的所有容器:
> ```bash
> docker ps -a
> ```
> 

| CONTAINER ID | IMAGE                  | COMMAND                | CREATED                 | STATUS           | PORTSNAME                                          |
|:-------------|:-----------------------|:-----------------------|:------------------------|:-----------------|:---------------------------------------------------|
| a1215e97a36c | docker/getting-started | "/docker-entrypoint.…" | About an hour ago       | Created          | lucid_liskov                                       |
| fcc9c7b01999 | docker/getting-started | "/docker-entrypoint.…" | &nbsp;About an hour ago | Up About an hour | 0.0.0.0:80-&gt;80/tcp&nbsp; &nbsp;trusting_swanson |

上表中 `a1215e97a36c/lucid_liskov` 即表示已终止容器。

> [!important]
> `STATUS` 的枚举值为:
> - `Created`: 表示已终止
> - `Up`: 表示运行中

## `docker start`

- [docker start](https://docs.docker.com/engine/reference/commandline/start/)

指定需要启动的已终止容器 `ID` 或容器名:

```bash
docker start CONTAINER
```

## `docker restart`

- [docker restart](https://docs.docker.com/engine/reference/commandline/restart/)

不论容器是否启动, 直接重启容器, 并指定需要重启容器的容器 `ID` 或容器名:

```bash
docker restart CONTAINER
```

# 终止容器

## 终止前保存容器状态

- [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)

使用 `docker stop` 命令, 并指定需要终止的容器 `ID` 或容器名:

```bash
docker stop CONTAINER
```

## 直接终止容器

- [docker kill](https://docs.docker.com/engine/reference/commandline/kill/)

使用 `docker kill` 命令, 并指定需要终止的容器 `ID` 或容器名:

```bash
docker kill CONTAINER
```

# `docker cp`

复制

# 创建容器

- [docker create](https://docs.docker.com/engine/reference/commandline/create/)

## 不指定容器名

由指定镜像 `IMAGE` 创建容器:

```bash
docker create IMAGE
# docker create docker/getting-started
```

按上述命令创建完容器后会打印一个容器 `ID`, 该 `ID` 为容器的唯一标识, 可根据该 `ID` 进行后续操作, 如终止、重启等。

> [!tip]
> 如果未指定容器名, 则 `docker` 会自动分配一个容器名。

## 指定容器名

由指定镜像 `IMAGE` 创建指定容器名 `CONTAINER` 的容器:

```bash
docker create --name CONTAINER IMAGE
```

# 删除容器

```bash
docker delete <IMAGE NAME>
```

## 查看容器日志

```bash
docker logs [OPTIONS] CONTAINER
# docker logs --details redis
```

# 容器状态

- `Created`
- `Running`
- `Pause`
- `Stopped`
- `Deleted`

# `WASM`

- [Docker+Wasm (Beta)](https://docs.docker.com/desktop/wasm/)