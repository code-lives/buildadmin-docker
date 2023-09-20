## 感谢 [BuildAdmin](https://github.com/build-admin/BuildAdmin) 开源项目

## 容器环境环境介绍

php8.2
node14
npm@6.14.0
pnpm@6.32.13

## 下载 docker-compose.yml 到项目根目录

如果没有有本地或远程数据库 把 docker-compose.yml 中的 mysql 注释解开即可，注意 mysql 连接有问题的话，mysql 地址就需要更换 127.0.0.1 或其他，使用本配置的 mysql，连接地址就是 mysql 不是 127.0.0.1

## 开始安装运行

```js
docker-compose up -d
```

## 进入容器

```js
docker exec -it location sh
```

## 直接 su 命令(容器内)

方便补 tab 等命令，不然很难受

```php
su
```

## 安装 vendor(容器内)

composer 可以会提示安装有问题，需要跳过之类，直接把提示的那段 composer install --ignore-platform-req=ext-calendar 加到 install 后面即可

```js
composer install
```

## 前端 node_model 安装，进入 web 文件夹(容器内)

```js
npm install
```

## 这样就可以访问了 127.0.0.1:8000

# 后台接口默认 8000,如何修改成 80 把 nginx.conf 也下载到项目根目录

## 后台 127.0.0.1/admin 前台 127.0.0.1

## Api 端口默认 80 如需修改成项目默认

nginx.conf 80 端口修改为 8000

## 前端请求接口是 8000，请修改 web/.env.development

```js
VITE_AXIOS_BASE_URL = "http://127.0.0.1";
```

## nginx 配置隐藏掉了 index.html 在把 web\src\router\index.ts 修改隐藏掉#号，不然 127.0.0.1/#/admin 看着就烦～ 😄

```js
import { createRouter, createWebHistory } from "vue-router";
import NProgress from "nprogress";
import "nprogress/nprogress.css";
import { staticRoutes } from "/@/router/static";
import { loading } from "/@/utils/loading";

const router = createRouter({
  history: createWebHistory(),
  routes: staticRoutes,
});
```
