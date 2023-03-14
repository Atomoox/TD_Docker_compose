FROM php:8.2-apache

RUN apt-get update && apt-get install -y nano
RUN docker-php-ext-install pdo_mysql
RUN mkdir -p /var/run/apache2/

#XDEBUG
WORKDIR /var/www/html/

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.mode=debug,profile" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_port=9003" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \

RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.mode=debug,profile" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.client_port=9003" >> /usr/local/etc/php/php.ini-development \

#Create phpinfo
RUN echo "<?php phpinfo(); ?>" >> /var/www/html/phpinfo.php
