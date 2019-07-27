FROM php:7.3.6-fpm-alpine

RUN set -ex && \
    # packages
    apk add --update --no-cache \
        postgresql-dev \
        libzip-dev \
        libxml2-dev && \
    # php ext
    docker-php-ext-install \
        zip \
        xml \
        simplexml \
        soap \
        mbstring \
        tokenizer \
        pdo \
        pdo_pgsql \
        pdo_mysql \
        pgsql \
        mysqli \
        bcmath && \
    # composer
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    # configuring php
    cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
    sed -i "/post_max_size = .*/c\post_max_size = 100M" /usr/local/etc/php/php.ini && \
    sed -i "/upload_max_filesize = .*/c\upload_max_filesize = 100M" /usr/local/etc/php/php.ini && \
    sed -i "/memory_limit = .*/c\memory_limit = -1" /usr/local/etc/php/php.ini

CMD ["php-fpm"]

EXPOSE 9000