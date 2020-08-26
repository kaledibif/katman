FROM php:7.4-fpm

COPY conf/ /usr/local/etc/php/conf.d/

RUN apt-get update \
    && apt-get -y --no-install-recommends install apt-utils curl zip unzip \
        procps git nano wget \
        zlib1g-dev libgpgme11 libgpgme11-dev \
        libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libreadline-dev \
        libgmp-dev libmhash-dev libpng-dev libxml2-dev libssl-dev libzip-dev libpq-dev \
        re2c apache2-utils openssl autoconf pkg-config

RUN docker-php-ext-install pdo_mysql opcache zip
RUN docker-php-ext-configure gd
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install soap mysqli intl bcmath pcntl
RUN docker-php-ext-configure gmp
RUN docker-php-ext-install gmp

RUN curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/bin --filename=composer && chmod +x /usr/bin/composer

USER root
RUN usermod -u 1000 www-data
EXPOSE 9000
WORKDIR /var/www/html
CMD ["php-fpm"]
