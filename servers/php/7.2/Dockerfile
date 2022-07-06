FROM php:7.2-fpm

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
        libssl-dev

RUN pecl install yaf-3.0.6 && docker-php-ext-enable yaf
RUN pecl install redis-5.0.0 && docker-php-ext-enable redis
RUN pecl install mcrypt-1.0.3 && docker-php-ext-enable mcrypt

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
RUN chown -R www-data /var/www/html

WORKDIR /var/www/html

EXPOSE 9000

CMD ["php-fpm"]