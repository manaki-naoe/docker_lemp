FROM php:7.3.12-fpm-alpine
LABEL maintainer "Manaki <manakinaoe@gmail.com>"

RUN set -xe && \
    apk add --no-cache --update \
        autoconf \
        bash \
        curl \
        ffmpeg \
        freetype \
        libjpeg-turbo \
        libmemcached \
        libmemcached-libs \
        libpng \
        libwebp \
        libxml2 \
        libxpm \
        libzip \
        zlib && \
    apk add --no-cache --update --virtual .phpize-deps \
        $PHPIZE_DEPS && \
    apk add --no-cache --update --virtual .memcached-deps \
        zlib-dev \
        libmemcached-dev \
        cyrus-sasl-dev && \
    apk add --no-cache --update --virtual .other-deps \
        freetype-dev \
        g++ \
        gcc \
        git \
        libjpeg-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libxpm-dev \
        libzip-dev \
        tzdata \
        zlib-dev && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-webp-dir=/usr/include/ \
        --with-xpm-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) \
        dom \
        gd \
        iconv \
        mbstring \
        mysqli\
        opcache \
        pdo_mysql \
        zip && \
    pecl install memcached && \
    docker-php-ext-enable \
        mysqli \
        pdo_mysql \
        memcached && \
    rm -rf /tmp/* && \
    apk del .phpize-deps .other-deps

COPY conf/php.ini /usr/local/etc/php/php.ini
COPY conf/www.conf /usr/local/etc/php-fpm.d/www.conf

#Composer install
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www