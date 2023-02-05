#Obsidian #Publish
# `Obsidian Publish`

 - [Obsidian Publish](https://obsidian.md/publish)

![Obsidian Publish](https://obsidian.md/images/publish-screenshot.png)

# `MindStone`

- [MindStone - GitHub](https://github.com/TuanManhCao/digital-garden)

```bash
git clone https://github.com/TuanManhCao/digital-garden.git

npm install --global yarn
```

![MindStone Demo](https://github.com/TuanManhCao/digital-garden/raw/main/public/images/CleanShot%202022-04-20%20at%2008.34.17@2x.png)

# `Prelite`

- [Prelite - GitHub](https://github.com/secure-77/Perlite)
- [Prelite Demo](https://perlite.secure77.de/)

![Prelite Demo](https://raw.githubusercontent.com/secure-77/Perlite/main/screenshots/screenshot.png)

## Docker

###  安装 `Docker`

https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

- 下载 `Docker`: [Get Docker](https://docs.docker.com/get-docker/)
- 终端运行 `wsl --update`
- 查看 `Docker` 版本: `docker -v`

### 操作步骤

- [02 Setup Docker](https://github.com/secure-77/Perlite/wiki/02---Setup-Docker)
- [03 Prelite Settings](https://github.com/secure-77/Perlite/wiki/03---Perlite-Settings#required-settings)
- [Optional (Backend) Settings](https://github.com/secure-77/Perlite/wiki/03---Perlite-Settings#optional-backend-settings)

1. 打开 `Docker` 客户端
2. 项目根目录下 (与 `docker-compose.yml` 同级) 运行 `docker-compose up -d`
3. 打开 `http://localhost/` 即可预览 `Web` 界面

> [!caution]
> 如果修改了 `cocker-compose.yml` 文件内容, 建议同步修改 `dpcker-compose-dev.yml` 文件内容。

### 修改根目录

> [!tip] 修改 `Obsidian` 笔记根目录 (入口目录)
> 项目根目录下 `docker-compose.yml`:
> ```yml
> services:
> 	perlite:
> 		environment:
> 			# - NOTES_PATH=Demo
> 			- NOTES_PATH=paranoiawhy
> 		volumes:
> 			# - ./perlite/Demo:/var/www/perlite/Demo:ro
> 			- ./perlite/paranoiawhy:/var/www/perlite/paranoiawhy:ro
> ```
> `Obsidian` 笔记根目录默认值为 **Demo**, 修改为 **paranoiawhy**

### 添加忽略文件夹

> [!tip] 添加忽略文件夹
> 项目根目录下 `docker-compose.yml`:
> ```yml
> services:
> 	perlite:
> 		environment:
> 			# - HIDE_FOLDERS=docs,private,trash
>       - HIDE_FOLDERS=docs,private,trash,Attachments
> ```
> 这里以 `Attachments` 文件夹为例。

### 本地开发调试

> [!tip] 本地开发调试
> 终端下输入以下命令:
> ```bash
> docker-compose --file docker-compose-dev.yml up -d
> ```
> 本地改动后无须重建 (`rebuild`)

## `Github Actions` 配置 `Docker`

```yaml
name: Docker Image CI

on:
  push:
    branches: [ "dev" ]
  pull_request:
    branches: [ "dev" ]

jobs:

  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Build the Docker image
      run: docker build . --file Dockerfile --tag my-image-name:$(date +%s)

```

# `docker hub`

- 账号: paranoiawhy
- 密码: why17375774285
- 邮箱: paranoiawhy@gmail.com

## `GitHub secrets`

- [Creating encrypted secrets for a repository](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)
- [Naming your secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#naming-your-secrets)

- DOCKERHUB_USERNAME: paranoiawhy
- DOCKERHUB_TOKEN

# 利用 `Github Actions` 构建和推送 `Docker` 镜像

- [GitHub Action: Build and push Docker images](https://github.com/marketplace/actions/build-and-push-docker-images)
- [Git context](https://github.com/marketplace/actions/build-and-push-docker-images#git-context)

# `Flowershow`

- [Flowershow](https://flowershow.app/)
- [Flowershow Docs](https://flowershow.app/docs)

![Flowershow Demo](https://github.com/flowershow/flowershow/raw/main/site/content/assets/images/obsidian_vs_flowershow.png)

# `Digital Garden`

- [Obsidian Digital Garden](https://github.com/oleeskild/obsidian-digital-garden)
- [Documentation and examples](https://dg-docs.ole.dev/)
- [EDAV Garden](https://edav-garden.netlify.app/)
- [notes.ole.dev](https://notes.ole.dev/)


> [!tip]
> 可在 `Obsidian` 插件市场中搜索 `GitHub Publisher`

![Digital Garden Demo](https://raw.githubusercontent.com/oleeskild/obsidian-digital-garden/main/img/dg-demo.gif)

# `Gatsby Garden`

- [Gatsby Garden](https://github.com/thex3family/gatsby-garden)
- [Gatsby Garden Demo](https://notes.binnyva.com/)
- [How to customize and publish your digital garden for free with obsidian and gatsby (Ep. 73)](https://www.youtube.com/watch?v=pm0mhkWj5ac)

# `Quartz`

- [Quartz - GitHub](https://github.com/jackyzha0/quartz)
- [Quartz Demo](https://quartz.jzhao.xyz/)

![Quartz Demo](https://github.com/jackyzha0/quartz/raw/hugo/screenshot.png)

# `linked-bolg-starter`

- [linked-bolg-starter](https://github.com/matthewwong525/linked-blog-starter)
- [linked-bolg-starter Demo](https://linked-blog-starter.vercel.app/home)

![linked-bolg-starter Demo](https://github.com/matthewwong525/linked-blog-starter/raw/main/common_md/attachments/fn-website-demo.gif)

# `Pubsidian`

- [Pubsidian GitHub](https://github.com/yoursamlan/pubsidian)
- [Pubsidian Demo](https://yoursamlan.github.io/pubsidian/)

![Pubsidian Demo](https://user-images.githubusercontent.com/33586885/128595527-d8799497-271a-4dab-9019-90b8346c9d61.png)

# `Obsidian GitHub Publisher`

- [Obsidian GitHub Publisher](https://github.com/ObsidianPublisher/obsidian-github-publisher)
- [Obsidian GitHub Publisher Demo](https://obsidian-publisher.netlify.app/)

> ![tip]
> 可在 `Obsidian` 插件市场中搜索 `GitHub Publisher`

# `Mkdocs`

- [Manim Library Tutorial for Math, Physics & Chemistry.](https://github.com/tarekshehata/alkashi)
- [Demo](https://tarekshehata.github.io/alkashi/)
- [My Obsidian & Mkdocs workflow](https://forum.obsidian.md/t/my-obsidian-mkdocs-workflow/24424)

![Demo](https://forum.obsidian.md/uploads/default/original/3X/2/5/25abdcca310a5be5a8d5c0fa77849450395c8a70.png)

# `Obsidian Plugin Developers Docs`

- [Obsidian Plugin Developers Docs - GitHub](https://github.com/marcusolsson/obsidian-plugin-docs)
- [Obsidian Plugin Developers Docs Demo](https://marcus.se.net/obsidian-plugin-docs/)

![[../Attachments/Obsidian Plugin Developers Docs Demo.png]]

> [!note]
> 技术栈:
> - `Docusaurus`

## 操作步骤

1. 安装依赖: `npm i`
2. 项目根目录下 (与 `package.json` 同级) 运行: `npm run start` [start - package.json](https://github.com/marcusolsson/obsidian-plugin-docs/blob/main/package.json#L7)
3. 打开 http://localhost:3000/obsidian-plugin-docs/ 即可预览 `Web` 界面

![[../Attachments/Obsidian Plugin Developers Docs 运行示意.png]]