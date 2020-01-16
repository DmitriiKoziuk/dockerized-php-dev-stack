FROM php:7.3.13-fpm

MAINTAINER Dmitrii Kozyuk <dmitrii.kozyuk@gmail.com>

RUN apt-get update && apt-get install -y \
        g++ \
        curl \
        wget \
        git \
        libfreetype6-dev \
        libjpeg-dev \
        libmcrypt-dev \
        libpng-dev \
        zip \
        libzip-dev \
        imagemagick \
        libmagickwand-dev \
        zlib1g-dev libicu-dev \
        graphviz \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && pecl install mcrypt-1.0.3 \
    && pecl install redis-5.1.1 \
    && pecl install xdebug-2.9.0 \
    && pecl install xhprof-2.1.4 \
    && pecl install imagick-3.4.4 \
    && docker-php-ext-enable mcrypt redis imagick xdebug xhprof

ENV PHP_IDE_CONFIG="serverName=php73dev"

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN groupadd -g 1000 dmitry \
    && useradd -r -d /var/www -s /bin/bash -g dmitry -G sudo -u 1000 dmitry \
    && mkdir /tmp/xhprof

USER dmitry:dmitry

WORKDIR /var/www

CMD ["php-fpm"]
