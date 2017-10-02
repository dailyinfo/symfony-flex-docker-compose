FROM php:7.1

MAINTAINER Daily Info <info@dailyinfo.co.uk>

RUN apt-get update && apt-get install -y \
    openssl \
    git \
    unzip \
    libmcrypt-dev
RUN docker-php-ext-install pdo pdo_mysql mcrypt

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN usermod -u 1000 www-data

WORKDIR /var/www/symfony