FROM ferimer/hosting:php7
MAINTAINER <devteam@ferimer.es>

RUN apt update && \
    apt dist-upgrade -y && \
    apt install -y unzip libzip-dev libxml2-dev && \
    apt autoremove -y && \
    docker-php-ext-install zip intl xmlrpc soap opcache

WORKDIR /var/www/html/
ADD https://www.prestashop.com/es/file/prestashop_1-7-7-4-zip/download?token=vT6runFc /opt/prestashop_1.7.7.4.zip
RUN unzip /opt/prestashop_1.7.7.4 && \
    chown -R www-data:www-data /var/www/html
VOLUME /var/www/html/
