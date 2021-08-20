FROM php:7.2-fpm

RUN apt-get --allow-releaseinfo-change update && buildDeps="libpq-dev libzip-dev" && apt-get install -y $buildDeps git nano wget vim libpcre3-dev libmcrypt-dev libmemcached-dev libmemcached11 libmemcachedutil2 libpng-dev rsync cron zlib1g-dev libicu-dev g++ libjpeg-dev libpng-dev ca-certificates libxml2-dev zip --no-install-recommends
RUN docker-php-ext-install pdo pdo_pgsql pgsql zip bcmath mbstring calendar
RUN docker-php-ext-install gettext
RUN pecl install memcached && docker-php-ext-enable memcached

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

RUN docker-php-ext-install soap

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/
RUN docker-php-ext-install gd && docker-php-ext-enable gd
RUN docker-php-ext-install opcache

RUN apt-get install -y locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    sed -i -e 's/# pl_PL.UTF-8 UTF-8/pl_PL.UTF-8 UTF-8/' /etc/locale.gen && \
    sed -i -e 's/# ro_RO.UTF-8 UTF-8/ro_RO.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN wget https://getcomposer.org/composer-stable.phar && mv composer-stable.phar /usr/bin/composer && chmod +x /usr/bin/composer

VOLUME /app
WORKDIR /app
