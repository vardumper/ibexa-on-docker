FROM docker.io/bitnami/php-fpm:8.2.8

ENV PHP_MEMORY_LIMIT="512M"

RUN apt update && apt upgrade -y
RUN apt install --no-install-recommends wget unzip nano ${PHPIZE_DEPS} make cmake gcc g++ libpcre2-posix2 libpcre2-dev -yq

# Haven't figured out the Redis part yet
# ...

# Install Composer
FROM composer:latest AS composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Install NodeJS and Yarn
FROM node:18.4 AS node
COPY --from=node /usr/local/bin/node /usr/local/bin/node
COPY --from=node /usr/local/include/node /usr/local/include/node
COPY --from=node /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node /opt/yarn-v*/bin/* /usr/local/bin/
COPY --from=node /opt/yarn-v*/lib/* /usr/local/lib/

# Copy entrypoint
COPY --from=node /usr/local/bin/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

RUN ln --symbolic ../lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
    && ln --symbolic ../lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx