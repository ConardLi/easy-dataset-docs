---
icon: desktop-arrow-down
---

# 安装和使用

目前 Easy Dataset 支持客户端、NPM、Docker 三种启动方式，所有启动方式均**完全在本地处理数据**，无需担心数据隐私问题。

### 客户端启动（适合新手）

为了解决各种本地部署的环境问题，可以直接用客户端启动，支持以下平台：

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NmVkMTkyZjk3ZWU1MzA4ODc0YTI3ZDQyODhiOTNlYzVfTHd2c2hoYzNabTNJWlcwM1NzOWxncFk1SDlUMHV2NVNfVG9rZW46V01DbWI2NG54b2lVTEN4WHZGZmNMZUpUbnBjXzE3NDcxMzQ3MjA6MTc0NzEzODMyMF9WNA" alt=""><figcaption></figcaption></figure>

可以直接到 [https://github.com/ConardLi/easy-dataset/releases](https://github.com/ConardLi/easy-dataset/releases) 下载适合自己系统的安装包：

<figure><img src=".gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

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

### Docker启动（适合私有部署）

如果你想自行构建镜像，在云服务或者内网环境私有部署，可以使用项目根目录中的 `Dockerfile`：

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
   docker run -d -p 1717:1717 -v {YOUR_LOCAL_DB_PATH}:/app/local-db --name easy-dataset easy-dataset
```

> **注意：** 请将 `{YOUR_LOCAL_DB_PATH}` 替换为你希望存储本地数据库的实际路径。
