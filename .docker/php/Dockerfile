FROM php:7.3-fpm-alpine

LABEL maintainer="Islasse Camille <camille@kiboko.fr>"

RUN apk add --update \
    make \
    curl \
    nodejs \
    yarn \
    icu-dev \
    libpng-dev

RUN docker-php-ext-install mysqli pdo pdo_mysql intl gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

ADD php.ini /etc/php/conf.d/
ADD php.ini /etc/php/cli/conf.d/
ADD php-fpm.conf /etc/php/php-fpm.d/
#ADD xdebug.ini  /etc/php/conf.d/

WORKDIR /var/www/monofony

EXPOSE 9000

CMD ["php-fpm", "-F"]