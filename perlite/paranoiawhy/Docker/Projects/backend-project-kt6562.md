# `redis`

- [redis -docker hub](https://hub.docker.com/_/redis)

## 安装 `redis`

```bash
docker run --name some-redis -d redis
```

## 在 `Docker` 中运行 `redis`

```bash
docker run --name redis -p 6379:6379 -d redis
```

## 在本地运行 `redis`

#TODO

# `Python`

## 安装 `Python`

> [!imporant]
> - [Python 3.9.13](https://www.python.org/downloads/release/python-3913/)
> - 下载 `3.9` 版本的 `python`
> - 选择 `Windows installer (64-bit)`
> - 安装时勾选 `Add Python 3.9 to Path`

命令行下输入 `python` 进行 `Python` 交互模式, 可输入 `exit()` 退出该模式。

## 查看 `Python` 版本

```bash
python -V # python --version
# Python 3.9.13
```

## 查看 `Python` 安装路径

`CMD` 下使用 `where`:

```cmd
where python
```

`PowerShell` 下使用 `where.exe`:

```powershell
where.exe python
```

> [!attention]
> 在 `PowerShell` 下 `where` 是 `Where-Object` 的别名 (`alias`), 因而须用 `where.exe` 查找 `python` 安装路径。
> 可通过 `Get-Command where` 查看 `where` 命令的详细信息。

# 安装 `yapf` 格式化工具

```bash
pip install yapf
```

> [!tip]
> 在 `VS Code` 配置 `Setting.json`:
> 
> ```json
> "python.formatting.provider": "yapf",
> ```

# 安装 `Python` 依赖

列出已有依赖包:

```bash
pip list
```

## 安装 `pipreqs`

```bash
pip install pipreqs
```

## 生成 `requirements.txt` 文件:

```bash
pipreqs .
```

> [!danger]
> UnicodeDecodeError: 'gbk' codec can't decode byte 0x80 in position 1854: illegal multibyte sequence

上述报错原因是编码方式, 可指定编码方式为 `utf8` :

```bash
pipreqs . --encoding=utf8
```

> [!info]
> INFO: Successfully saved requirements file in .\requirements.txt

`requirements.txt` 内容示意:

> [!example]
> ```txt
> aiohttp==3.8.3
> aioredis==2.0.1
> jaydebeapi==1.2.3
> JPype1==1.4.1
> PyJWT==2.6.0
> ```

## 安装相应依赖

根据生成的 `requirements.txt` 文件安装相应的 `Python` 依赖:

```bash
pip install -r requirements.txt
```

## 参考链接

- [Python 项目如何生成 requirements.txt 文件](https://www.cnblogs.com/wintest/p/12813246.html)

# 本地运行 `Python` 项目

> [!attention]
> 在本地运行 `Python` 项目之前, 须运行 `redis` 。

`app.py`:

```python
# redis 配置
REDIS_URL = os.environ.get('REDIS_URL', 'redis://localhost:6379')

web.run_app(app, host='localhost', port=8080, access_log=None)
```

`VS Code` 打开 `app.py`, 右键 `Run Code (Ctrl + Alt + N)` 即可。

# 在 `Docker` 中运行 `Python` 项目

> [!attention]
> 在 `Docker` 中运行 `Python` 项目之前, 须运行 `redis` 。

`app.py` 应修改如下:

```python
# redis 配置
# REDIS_URL = os.environ.get('REDIS_URL', 'redis://localhost:6379')
REDIS_URL = os.environ.get('REDIS_URL', 'redis://10.10.21.86:6379')

# web.run_app(app, host='localhost', port=8080, access_log=None)
web.run_app(app, host='0.0.0.0', port=8080, access_log=None)
```

## 构建镜像

```bash
docker build -t python .
```

> [!attention]
> - `.` 表示上下文 `context`, 不可简单理解为 `Dockerfile` 文件路径
> - 如果不额外指定 `Dockerfile` 文件路径, `Docker` 会将上下文目录中的 `Dockerfile` 作为 `Dockerfile`
> - 可通过 `--file` 或 `-f`指定 `Dockerfile` 文件路径
> - 如果有文件不需要传递给 `Docker` 引擎, 可在 `.dockerignore` 中进行配置

## 运行到容器

```bash
docker run --name python -p 8080:8080 -d python
```

# 使用 `docker-compose.yml`

- [Quick Start](https://github.com/docker/compose#quick-start)
- [Docker Compose 使用](https://yeasy.gitbook.io/docker_practice/compose/usage)

`docker-compose.yml` :

```yml
version: '3'

services:
  # redis
  redis:
    image: "redis:alpine"

  # python
  python:
    build: .
    ports:
      - "8080:8080"
    environment:
      - REDIS_URL=redis://10.10.21.86:6379
    depends_on:
      - redis
```

## 运行

```bash
docker-compose up
```

## 实时查看运行输出:

```bash
docker logs -f CONTAINER
```

> [!tip]
> - `--follow` / `-f` 表示实时跟随输出
> - 可通过 `Ctrl + C` 关闭退出实时查看输出会话, 或者直接关闭终端

## 终止

```bash
docker-compose
```

# 本地调用 `api`

> [!tip]
> 以登录 `login` 为例, 请求的`URL` 应为:
> - `http://localhost:8080/login`
> - 其他请求同理。

# `Another Redis Desktop Manager`

- [Another Redis Desktop Manager - Github](https://github.com/qishibo/AnotherRedisDesktopManager)
- [releases](https://github.com/qishibo/AnotherRedisDesktopManager/releases)