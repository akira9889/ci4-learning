FROM php:8.1-apache

WORKDIR /var/www/html

RUN apt-get update \
  && apt-get install -y libonig-dev libzip-dev libicu-dev unzip mariadb-client vim \
  && a2enmod rewrite \
  && docker-php-ext-install intl pdo_mysql mysqli mbstring zip \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1

COPY ./docker/apache/httpd.conf /etc/apache2/sites-available/000-default.conf

COPY ./src /var/www/html
