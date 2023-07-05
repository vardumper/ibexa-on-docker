FROM docker.io/bitnami/minideb:bullseye

ENV APP_VERSION="8.2.7"
ENV PHP_MEMORY_LIMIT="512M"

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

RUN docker-php-ext-install gd intl xsl pdo_mysql xml \
    pecl install xdebug \
    docker-php-ext-enable xdebug