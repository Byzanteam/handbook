# How to build

这里列举一些一个项目应该怎样组织的建议

### README

一个介绍我是干嘛的 markdown 文件


### Makefile

我提供一些基本的 CLI 功能

- make init: 初始化项目及环境（创建并迁移数据库，初始化其它的项目依赖如 Elasticsearch/Minio 等）
- make build: build 项目（executable binary, compiled JavaScripts/CSS or docker images）
- make push: 推送项目的 built assets 至仓库（如推送 docker image 至 阿里云容器镜像服务）
- make release: 若项目为 包/库，将其最新版本发布到 包/库托管 上（如将库发布至 npm）
- make test: 运行项目测试
- make deploy: 部署项目
- make start/restart/stop: 运行/重启/终止 项目
- make status: 查看项目的运行状态

#### Tips

1. Makefile 只能用 `Tab` 做缩进
1. 出现 `make: 'target' is up to date` 错误时，使用 `.PHONY target` 将目标 `target` 加入到伪目标中
1. 在命令的开头加上 `@` 来隐藏不需要显示的命令（`@echo 'Deployment is done.'`）
1. 需要较多环境变量时，将这些环境变量制作成 `Makefile`（类似 docker 的 env file），使用 `include/-include` 将其引入
1. 通过注释自动生成帮助信息：
```makefile
.PHONY push help

push: ## push latest built docker images to image repository
	# do something

help:
	@perl -nle'print $& if m{^[a-zA-Z_-]+:.*?## .*$$}' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
```


### 构建容器

项目的环境

1. 将开发环境产生的、在构建镜像时不需要的文件/目录列入至 `.dockerignore` 中
1. 构建用于生产环境的镜像时，使用 `alpine` 版本的 base image（如 elixir:1.8.1-alpine）以减小生成镜像的大小
1. 使用 [Multi-stage build](https://docs.docker.com/develop/develop-images/multistage-build/) 进行构建，最终只保留有用的生成物以减小生成镜像的大小
1. 先复制管理依赖的文件并获取/编译依赖，再复制项目整体，最大程度利用 docker 的缓存机制节省构建时间和重新 push 镜像时间

#### 例子

```Dockerfile
# This should match the version of Alpine that node:10.15.2-alpine uses.
ARG ALPINE_VERSION=3.8

# Use alpine-version of node image to reduce size
FROM node:10.15.2-alpine AS builder

ARG APP_NAME
ARG APP_VSN

ENV APP_NAME=${APP_NAME} \
  APP_VSN=${APP_VSN}

WORKDIR /opt/app

# install dependencies before building our app
COPY package.json package.json 
COPY yarn.lock yarn.lock 
RUN yarn install

COPY . .

ENV NODE_ENV=production
RUN yarn build
RUN cp -r dist /opt/built

# Use multi-stage build
FROM alpine:${ALPINE_VERSION}

ARG APP_NAME=my_app

ENV REPLACE_OS_VARS=true \
    APP_NAME=${APP_NAME}

WORKDIR /opt/app

COPY --from=builder /opt/built .

CMD cp -r /opt/app /data
```



### WIKI

这个项目的一些 wiki 信息，方便其他人查看，应包含不局限于以下几个部分：

- document
- how to run
- how to build
- how to deploy


### CI
- CodeClimate：代码质量检测
- CircleCI：自动测试
  - 单元测试等
  - 覆盖率
