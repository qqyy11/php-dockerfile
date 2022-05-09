ARG VERSION=8.0
FROM php:${VERSION}-fpm-alpine
## 修改为国内仓库(清华镜像站)
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
    && apk upgrade \
## 加载 php 编译扩展， 以及 libtool
    && apk add --no-cache $PHPIZE_DEPS libtool curl-dev \
    && export PHPIZE_DEL=$PHPIZE_DEPS \
    && docker-php-ext-install bcmath pdo_mysql mysqli sockets \
    && pecl channel-update pecl.php.net
## 安装 zip
RUN apk add --no-cache libzip-dev \
    && docker-php-ext-install zip
## php 配置
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
## 安装 gd 库
RUN apk add --no-cache libpng libpng-dev libjpeg-turbo-dev \
    && docker-php-ext-configure gd && docker-php-ext-install gd 
## 安装 imagick
RUN apk add --no-cache --virtual .imagick-runtime-deps imagemagick-dev imagemagick \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && export PHPIZE_DEL=$(echo "$PHPIZE_DEL"|sed 's/g++//g')
## 安装 composer
RUN php -r "readfile('https://install.phpcomposer.com/installer');"|php \
    && mv composer.phar /usr/bin/composer
## 删除不需要的包
RUN apk del $PHPIZE_DEL curl-dev
