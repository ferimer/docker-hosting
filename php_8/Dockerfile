FROM php:8-apache
MAINTAINER <devteam@ferimer.es>

COPY ferimer_php_entrypoint /usr/local/bin/

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libgmp-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli pdo_mysql \
    && docker-php-ext-install gmp

ENTRYPOINT ["ferimer_php_entrypoint"]
CMD ["apache2-foreground"]
