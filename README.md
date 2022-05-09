# php-dockerfile

在官方 php 镜像基础上添加了一些扩展

## 构建 php 镜像

    # 命令
    docker build --build-arg VERSION=[version] -t testphp:[version] ./php
    # 示例
    docker build --build-arg VERSION=8.0 -t myphp:8.0 ./php

## 构建带有 swoole, imagick 的镜像

    # 命令
    docker build --build-arg VERSION=[version] -t testphp:[version] ./php-permium
    # 示例
    docker build --build-arg VERSION=8.0 -t myphp:8.0-permium ./php-permium
