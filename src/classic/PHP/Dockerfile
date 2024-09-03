FROM php:8.3-apache-bookworm
LABEL authors="Artem Plekhanov"

# Переменные сборки (установлены дефолтные значения)
ARG SERVER_USER=www-data
ARG SERVER_USER_UID=1001
ARG SERVER_GROUP=www-data
ARG SERVER_GROUP_UID=1001

# Конфигурация PHP
RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN apt-get update -y && apt-get install -y sendmail
RUN apt-get install -y libwebp-dev libjpeg62-turbo-dev libpng-dev libxpm-dev libfreetype6-dev
RUN docker-php-ext-configure gd --with-jpeg --with-freetype
RUN docker-php-ext-install gd

# Установка Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Конфигурация PHP-Apache образа
RUN a2dismod --force autoindex
RUN a2enmod rewrite

RUN usermod -u ${SERVER_USER_UID} ${SERVER_USER}
RUN groupmod -g ${SERVER_GROUP_UID} ${SERVER_GROUP}
RUN chown ${SERVER_USER}:${SERVER_GROUP} /var/www -R
RUN chmod 776 /var/www -R

RUN mkdir /var/log/php
RUN chmod 777 /var/log/apache2 -R
RUN chmod 777 /var/log/php -R

WORKDIR /var/www