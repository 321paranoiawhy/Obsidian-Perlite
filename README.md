# Obsidian-Perlite

![GitHub](https://img.shields.io/github/license/321paranoiawhy/Obsidian-Perlite) ![GitHub last commit](https://img.shields.io/github/last-commit/321paranoiawhy/Obsidian-Perlite)

```bash
# docker-compose.yml
docker-compose up -d

# docker-compose-dev.yml
docker-compose --file docker-compose-dev.yml up -d
```

服务器安装 `Docker`:

```bash
sudo wget -qO- https://get.docker.com/ | bash
```

启动 `Docker` 并设置为开机自启:

```bash
systemctl start docker
```

服务器安装 `Docker-Compose`:

```bash
# 下载 1.24.1 版本
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 将可执行权限应用于二进制文件
sudo chmod +x /usr/local/bin/docker-compose

# 创建软链
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

# 查看版本
docker-compose --version
```

拉取 `paranoiawhy/obsidian-frontend` 和 `paranoiawhy/obsidian-backend` 镜像:

```bash
docker pull paranoiawhy/obsidian-frontend:latest

docker pull paranoiawhy/obsidian-backend:latest
```

运行容器:

```bash
docker run --name obsidian-frontend -itd  -p 1234:1234 paranoiawhy/obsidian-frontend

# docker run --name perlite -itd -p 9000:9000 paranoiawhy/obsidian-backend
docker run --name obsidian-backend -itd -p 9000:9000 paranoiawhy/obsidian-backend
```

查看运行中的容器:

```bash
docker container ls
```

# Thanks to

- [Persite - GitHub](https://github.com/secure-77/Perlite)
- [Persite Demo](https://perlite.secure77.de/)
