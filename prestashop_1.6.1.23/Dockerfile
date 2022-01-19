FROM php:5.6-apache
MAINTAINER <devteam@ferimer.es>

COPY ferimer_php_entrypoint /usr/local/bin/

RUN a2enmod rewrite

RUN apt update && \
    apt dist-upgrade -y && \
    apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \

        libmcrypt-dev \
        libxml2-dev \
        libicu-dev \
        openssl \

        unzip \
        libzip-dev \
    && apt autoremove -y \
    && docker-php-source extract \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) mysqli pdo_mysql \
    && docker-php-ext-install -j$(nproc) zip intl xmlrpc soap opcache \
    && docker-php-source delete

WORKDIR /var/www/html/
ADD https://www.prestashop.com/es/system/files/ps_releases/prestashop_1.6.1.23.zip?token=0643346103 /opt/prestashop_1.6.1.23.zip
RUN unzip /opt/prestashop_1.6.1.23 && \
    chown -R www-data:www-data /var/www/html
VOLUME /var/www/html/

ENTRYPOINT ["ferimer_php_entrypoint"]
CMD ["apache2-foreground"]
