FROM php:7.4-fpm
LABEL maintainer="Aranoch"

ENV TZ=Asia/Shanghai

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin libpng-dev python2 libfreetype6-dev libjpeg-dev libpng-dev zlib1g-dev libzip-dev libbz2-dev \
    && docker-php-ext-install zip pdo pdo_mysql gd exif pcntl opcache bcmath \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && curl -L -o /tmp/redis.tgz https://pecl.php.net/get/redis-4.2.0.tgz \
    && tar -zxvf /tmp/redis.tgz -C /tmp \
    && mkdir -p /usr/src/php/ext/redis \
    && cp -r /tmp/redis-4.2.0/* /usr/src/php/ext/redis \
    && cd /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*