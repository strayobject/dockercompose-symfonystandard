FROM php:7.1-fpm

MAINTAINER Michal Zdrojewski <code@strayobject.co.uk>

RUN usermod -u 1000 www-data

# temporarily compile new version as debian has an outdated one
RUN curl -sS -o /tmp/icu.tar.gz -L http://download.icu-project.org/files/icu4c/57.1/icu4c-57_1-src.tgz && tar -zxf /tmp/icu.tar.gz -C /tmp && cd /tmp/icu/source && ./configure --prefix=/usr/local && make && make install

RUN apt-get update \
 && apt-get install -y unzip git libcurl4-gnutls-dev zlib1g-dev libicu-dev g++ \
 && docker-php-ext-configure intl --with-icu-dir=/usr/local \
 && docker-php-ext-install pdo pdo_mysql sockets zip json intl \
 && apt-get autoremove && apt-get autoclean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY opt/php71/conf/conf.d/*.ini /usr/local/etc/php/conf.d/
COPY opt/php71/conf/php.ini /usr/local/etc/php/php.ini
