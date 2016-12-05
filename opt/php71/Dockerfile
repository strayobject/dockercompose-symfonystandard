FROM php:7.1-rc-fpm

MAINTAINER Michal Zdrojewski <code@strayobject.co.uk>

COPY opt/php71/*.ini /usr/local/etc/php/conf.d/

RUN usermod -u 1000 www-data

RUN apt-get update \
 && apt-get install -y unzip git libcurl4-gnutls-dev zlib1g-dev libicu-dev g++ \
 && docker-php-ext-install pdo pdo_mysql sockets zip json \
 && apt-get autoremove && apt-get autoclean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

