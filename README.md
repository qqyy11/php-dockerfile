# php-dockerfile
## 构建 php 镜像

    # 命令
    docker build --build-arg VERSION=[version] -t testphp:[version] ./php
    # 示例
    docker build --build-arg VERSION=8.0 -t myphp:8.0 ./php

## 构建带有 swoole 的镜像

    # 命令
    docker build --build-arg VERSION=[version] -t testphp:[version] ./php-swoole
    # 示例
    docker build --build-arg VERSION=8.0 -t myphp:8.0-swoole ./php-swoole
