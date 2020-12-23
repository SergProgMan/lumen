FROM php:fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        exiftool \
        libcurl4-openssl-dev \
        libssl-dev \
        libzip-dev \
        libpq-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && docker-php-ext-install iconv \
    && docker-php-ext-install exif \
    && docker-php-ext-install zip \
    && docker-php-ext-install pgsql \
    && docker-php-ext-install pdo_pgsql

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN chmod a+x composer.phar
RUN mv composer.phar /usr/local/bin/composer

WORKDIR /application

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY custom-php.ini $PHP_INI_DIR/conf.d/

