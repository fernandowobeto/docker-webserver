FROM php:7.4-fpm

RUN apt-get update

# Install iconv, mcryot, gd
RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y libjpeg62-turbo-dev
RUN apt-get install -y libmcrypt-dev
RUN apt-get install -y libpng-dev
RUN apt-get install -y libzip-dev
RUN apt-get install -y libonig-dev

RUN docker-php-ext-install -j$(nproc) iconv
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

# Install intl
RUN apt-get install -y libicu-dev
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y g++

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

# Install mbstring
RUN docker-php-ext-install mbstring

# Install curl
RUN apt-get install -y libcurl4-openssl-dev
RUN docker-php-ext-install curl

# Install zip
RUN docker-php-ext-install zip

# Install json
RUN docker-php-ext-install json

# Install extensions through the scripts the container provides
# Here we install the pdo_mysql extensions to access MySQL.
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN docker-php-ext-enable mysqli

RUN apt-get install -y libpq-dev
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install pdo pdo_pgsql pgsql

#opcache.validate_timestamps - production environments: 0
RUN usermod -u 1000 www-data
RUN echo 'date.timezone="America/Sao_Paulo"' >> /usr/local/etc/php/conf.d/date.ini
RUN echo 'opcache.enable=1' >> /usr/local/etc/php/conf.d/opcache.conf
RUN echo 'opcache.validate_timestamps=1' >> /usr/local/etc/php/conf.d/opcache.conf
RUN echo 'opcache.fast_shutdown=1' >> /usr/local/etc/php/conf.d/opcache.conf