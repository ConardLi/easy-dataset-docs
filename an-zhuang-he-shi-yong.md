---
icon: desktop-arrow-down
---

# 安装和使用

目前 Easy Dataset 支持客户端、NPM、Docker 三种启动方式，所有启动方式均**完全在本地处理数据**，无需担心数据隐私问题。

### 客户端启动（适合新手）

为了解决各种本地部署的环境问题，可以直接用客户端启动，支持以下平台：

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

可以直接到 [https://github.com/ConardLi/easy-dataset/releases](https://github.com/ConardLi/easy-dataset/releases) 下载适合自己系统的安装包：

如果遇到 Github 下载较慢，可以使用网盘下载：[https://pan.quark.cn/s/ef8d0ef3785a](https://pan.quark.cn/s/ef8d0ef3785a)&#x20;

<figure><img src=".gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

***

### NPM 启动（适合开发者）

本项目基于 Next 构建，所以本地只要有 Node 环境就可以通过 NPM 直接启动，适合开发者，需要调试项目的同学：

1. 克隆仓库：

```bash
   git clone https://github.com/ConardLi/easy-dataset.git
   cd easy-dataset
```

2. 安装依赖：

```bash
   npm install
```

3. 启动服务器：

```bash
   npm run build
   npm run start
```

{% hint style="warning" %}
注意：使用 NPM 启动的情况下，当系统发布新版本后，需要重新执行 `git pull` 拉取最新代码，并且重新执行 `npm install`、`npm run build`、`npm run start` 三个步骤。
{% endhint %}

***

### Docker 启动 - 使用官方 Docker 镜像（适合私有部署）

1. 克隆仓库：

```bash
git clone https://github.com/ConardLi/easy-dataset.git
cd easy-dataset
```

2. 更改 `docker-compose.yml` 文件：

```yml
services:
  easy-dataset:
    image: ghcr.io/conardli/easy-dataset
    container_name: easy-dataset
    ports:
      - '1717:1717'
    volumes:
      - ./local-db:/app/local-db
      # - ./prisma:/app/prisma 如果需要挂载请先手动初始化数据库文件
    restart: unless-stopped
```

> **注意：** 请将 `{YOUR_LOCAL_DB_PATH}`、`{LOCAL_PRISMA_PATH}` 替换为你希望存储本地数据库的实际路径，建议直接使用当前代码仓库目录下的 `local-db` 和 `prisma` 文件夹，这样可以和 NPM 启动时的数据库路径保持一致。

> **注意：** 如果需要挂载数据库文件（PRISMA），需要提前执行 `npm run db:push` 初始化数据库文件。

3. 使用 docker-compose 启动

```bash
docker-compose up -d
```

4. 打开浏览器并访问 `http://localhost:1717`

***

### Docker 启动 - 手动打包（适合私有部署）

如果你想自行构建镜像，可以使用项目根目录中的 Dockerfile：

1. 克隆仓库：

```bash
git clone https://github.com/ConardLi/easy-dataset.git
cd easy-dataset
```

2. 构建 Docker 镜像：

```bash
docker build -t easy-dataset .
```

3. 运行容器：

```bash
docker run -d \
  -p 1717:1717 \
  -v {YOUR_LOCAL_DB_PATH}:/app/local-db \
  -v {LOCAL_PRISMA_PATH}:/app/prisma \
  --name easy-dataset \
  easy-dataset
```

> **注意：** 请将 `{YOUR_LOCAL_DB_PATH}`、`{LOCAL_PRISMA_PATH}` 替换为你希望存储本地数据库的实际路径，建议直接使用当前代码仓库目录下的 `local-db` 和 `prisma` 文件夹，这样可以和 NPM 启动时的数据库路径保持一致。

4. 打开浏览器，访问 `http://localhost:1717`
