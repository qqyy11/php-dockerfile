ARG VERSION=8.0
FROM php:${VERSION}-fpm-alpine
## 修改为国内仓库(清华镜像站)
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
    && apk upgrade \
## 加载 php 编译扩展， 以及 libtool
    && apk add --no-cache --virtual .php-build-deps $PHPIZE_DEPS libtool curl-dev \
    && docker-php-ext-install bcmath pdo_mysql mysqli sockets \
    && pecl channel-update pecl.php.net \
## 安装 zip
    && apk add --no-cache libzip-dev \
    && apk add --no-cache --virtual .zip-runtime-deps libzip \
    && docker-php-ext-install zip \
    && apk del libzip-dev \
## php 配置
    && cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini \
## 安装 gd 库
    && apk add --no-cache --virtual .gd-build-deps libjpeg-turbo-dev \
    && apk add --no-cache --virtual .gd-runtime-deps libpng-dev \
    && docker-php-ext-configure gd && docker-php-ext-install gd \ 
    && apk del .gd-build-deps \
## 删除不需要的包
    && apk del .php-build-deps
## 添加一些扩展
RUN apk add --no-cache --virtual .php-build-deps $PHPIZE_DEPS libtool curl-dev
## 添加 imagick
RUN apk add --no-cache --virtual .imagick-runtime-deps imagemagick libgomp \
    && apk add --no-cache --virtual .imagick-build-deps imagemagick-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
## 添加swoole
    && pecl install -D 'enable-sockets="no" enable-openssl="yes" enable-http2="yes" enable-mysqlnd="yes" enable-swoole-json="no" enable-swoole-curl="yes" enable-cares="yes"' swoole \
    && docker-php-ext-enable swoole

## 安装 composer
RUN php -r "readfile('https://install.phpcomposer.com/installer');"|php \
    && mv composer.phar /usr/bin/composer
