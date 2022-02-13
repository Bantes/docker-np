FROM php:5.6-fpm
LABEL maintainer="Aranoch"

ENV TZ=Asia/Shanghai

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y \
       libfreetype6-dev \
       libjpeg62-turbo-dev \
       libpng-dev \
       zlib1g-dev \
       libzip-dev \
       libmcrypt-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip mcrypt pdo pdo_mysql \
    && curl -L -o /tmp/redis.tgz https://pecl.php.net/get/redis-4.2.0.tgz \
    && tar -zxvf /tmp/redis.tgz -C /tmp \
    && mkdir -p /usr/src/php/ext/redis \
    && cp -r /tmp/redis-4.2.0/* /usr/src/php/ext/redis \
    && cd /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*