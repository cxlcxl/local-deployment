FROM php:7.0-fpm

MAINTAINER silent <cxl_orange_man@163.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libjpeg-dev \
        pkg-config \
        libmcrypt-dev \
        libcurl4-openssl-dev \
        libssl-dev \
      &&  docker-php-ext-install -j$(nproc) iconv mcrypt

RUN pecl install yaf-3.0.4 && docker-php-ext-enable yaf
RUN pecl install redis-3.0.0 && docker-php-ext-enable redis

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
# 解决本地虚拟机共享文件夹权限问题
RUN groupadd --gid 994 vboxsf
RUN usermod -aG vboxsf www-data

WORKDIR /var/www/html

EXPOSE 9000

CMD ["php-fpm"]