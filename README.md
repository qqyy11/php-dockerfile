# php-dockerfile

在官方 php 镜像基础上添加了一些扩展

## 构建 php 镜像

### 参数

- `PHP_TAG`  继承的 php 镜像的 tag 默认使用 8.0-fpm-alpine
- `SWOOLE`   是否安装 swoole 扩展默认 1 ，1：安装；0：不安装 
- `IMAGIC`   是否安装 imagic 扩展默认 1 ，1：安装；0：不安装 
- `COMPOSER` 是否安装 composer 默认 1 ，1：安装；0：不安装 

### 构建命令示例
    # 命令
    docker build --build-arg PHP_TAG=[tag] --build-arg SWOOLE=1 --build-arg IMAGIC=1 --build-arg COMPOSER=1 -t [you image]:[you tag] ./php
    # 示例
    docker build --build-arg PHP_TAG=8.0-fpm-alpine --build-arg SWOOLE=1 --build-arg IMAGIC=1 --build-arg COMPOSER=1 -t myphp:8.0 ./php

