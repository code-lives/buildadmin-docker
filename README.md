## 感谢 [BuildAdmin](https://github.com/build-admin/BuildAdmin) 开源项目

基于 docker 快速部署环境（php8.2、node14、npm@6.14.0、nnpm@6.32.13）

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

## 进入容器直接 su 命令

方便补 tab 等命令，不信的话你试试（试试就逝世 ）😄

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

这样就可以访问了 127.0.0.1:8000

# 后台接口默认 8000,如何修改成 80

1. 把 nginx.conf 也下载到项目根目录

2. 把 docker-compose.yml 的 nginx 注释解开端口 8000 修改为 80

3. 前端请求接口 8000，请修改 web/.env.development 改为 VITE_AXIOS_BASE_URL = 'http://localhost'

# htts 如何配置，查看 nginx.conf 把域名、证书更换，解开注释即可用

## Docker 注意问题

1. 如果运行在服务器，需要最低 2G 内存-4G 内存，因为项目加容器就 1G 左右，还要运行其他。

2. 正式项目，不推荐用 docker 部署 mysql

## Thinkphp 问题

#### 发现自己写的接口 调试没反应。那就在 接口后面加 server=1

原理 查看 nginx.conf 就看到 server 参数设置

http://127.0.0.1/admin/index/index?server=1
