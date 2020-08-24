FROM php:7.2-fpm-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
	&& apk update \
	&& apk add --no-cache --update --virtual .phpize-deps $PHPIZE_DEPS \
	&& apk add --no-cache --update libwebp-dev libpng-dev freetype-dev libjpeg-turbo-dev libxpm-dev \
	&& docker-php-ext-install -j$(nproc) mysqli pdo_mysql \
	&& pecl install -o -f redis \
	&& docker-php-ext-enable redis \
	&& docker-php-ext-configure gd --with-webp-dir=/usr/include/ --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ --with-xpm-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& apk del  .phpize-deps \
	&& rm -rf /var/cache/apk/*  /var/lib/apk/* /etc/apk/cache/* /tmp/* /usr/share/php
