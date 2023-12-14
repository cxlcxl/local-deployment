FROM php:7.4-fpm

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libwebp-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libjpeg-dev \
        pkg-config \
        libmcrypt-dev \
        libcurl4-openssl-dev \
        zlib1g-dev \
        libzip-dev \
        libssl-dev \
        libmagickwand-dev \
        libmagickcore-dev \
        librdkafka1 librdkafka-dev

RUN apt-get install -y unixodbc-dev && rm -rf /var/lib/apt/lists/*

RUN docker-php-source extract
RUN docker-php-ext-configure pdo_odbc --with-pdo-odbc=unixODBC,/usr
RUN docker-php-ext-install pdo_odbc 
RUN set -x \
    && cd /usr/src/php/ext/odbc \
    && phpize \
    && sed -ri 's@^ *test +"\$PHP_.*" *= *"no" *&& *PHP_.*=yes *$@#&@g' configure \
    && ./configure --with-unixODBC=shared,/usr \
    && docker-php-ext-install odbc

# libmagickwand-dev libmagickcore-dev --> imagick 所需
# unixodbc-dev -->  odbc pdo_odbc 所需

RUN pecl install redis-4.0.0 && docker-php-ext-enable redis
RUN pecl install mcrypt-1.0.3 && docker-php-ext-enable mcrypt
RUN pecl install swoole-4.4.15 && docker-php-ext-enable swoole
RUN pecl install SeasLog-2.2.0 && docker-php-ext-enable seaslog
RUN pecl install imagick-3.7.0 && docker-php-ext-enable imagick
RUN pecl install rdkafka-6.0.0 && docker-php-ext-enable rdkafka

RUN docker-php-ext-install fileinfo pcntl sockets

RUN apt-get update \
    && apt-get -y install libpq-dev \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

#RUN docker-php-ext-install pdo_pgsql
#RUN docker-php-ext-install pdo
RUN docker-php-ext-install gd
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install zip
RUN docker-php-ext-install bcmath

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

WORKDIR /var/www/html

EXPOSE 9000

CMD ["php-fpm"]