FROM docker.io/bitnami/php-fpm:8.2.8

ENV PHP_MEMORY_LIMIT="512M"

RUN apt-get update && apt-get upgrade -y
RUN apt-get install --no-install-recommends wget=1.21 unzip=6.00 nano=5.4 "${PHPIZE_DEPS}" make=4.3 cmake=3.18.4 gcc=10.2.1 g++=10.2.1 libpcre2-posix2 libpcre2-dev -yq

# Haven't figured out the Redis part yet
# ...

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Install NodeJS and Yarn
COPY --from=node:18.4 /usr/local/bin/node /usr/local/bin/node
COPY --from=node:18.4 /usr/local/include/node /usr/local/include/node
COPY --from=node:18.4 /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node:18.4 /opt/yarn-v*/bin/* /usr/local/bin/
COPY --from=node:18.4 /opt/yarn-v*/lib/* /usr/local/lib/

# Copy entrypoint
COPY --from=node /usr/local/bin/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

RUN ln --symbolic ../lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
    && ln --symbolic ../lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx